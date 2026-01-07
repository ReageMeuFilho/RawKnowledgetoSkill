# Skill Specification: Voice & Communication Intelligence Platform

> **Skills Covered**: SKILL-109, SKILL-110, SKILL-111, SKILL-113, SKILL-114, SKILL-115
> **Category**: Voice / Communication / AI
> **Phase**: Phase 2 - Group 4 (Voice & Communication)
> **Priority**: P2 (Enhanced)
> **Status**: SPECIFIED
> **Last Updated**: January 2026
> **Research Source**: Research Phase 2 Group 4.txt (~12,800 lines)

---

## 📋 EXECUTIVE SUMMARY

The Voice & Communication Intelligence Platform delivers **6 advanced voice skills** that transform property communication from basic telephony into an enterprise-grade voice AI system:

- **<300ms** transcription latency (real-time ASR)
- **53.4%** lower word error rate vs competitors (Deepgram Nova-3)
- **48+** emotion dimensions detected (Hume AI EVI)
- **100%** TCPA compliance for outbound campaigns
- **100+ languages** supported with code-switching

### Skills Overview

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| **SKILL-109** | Call Recording Transcription | Voice Processing | Real-time ASR with speaker diarization |
| **SKILL-110** | Voicemail Intelligence | Communication | Automated transcription with urgency detection |
| **SKILL-111** | Voice Sentiment Analysis | AI Analytics | Real-time emotion detection and escalation |
| **SKILL-113** | Multi-Language Voice | Localization | 100+ languages with code-switching |
| **SKILL-114** | Outbound Calling Campaigns | Compliance | TCPA-compliant automated campaigns |
| **SKILL-115** | IVR Flow Builder | User Interface | Visual drag-and-drop flow designer |

---

## 🏗️ ARCHITECTURE ALIGNMENT NOTES

### Layer Mapping (Citadel OS 6-Layer Stack)

| Component | Citadel OS Layer | Implementation |
|-----------|------------------|----------------|
| IVR Flow Builder UI | Layer 6: Applications | React + TypeScript |
| Voice Domain | Layer 5: Domain Bundles | Voice communication bundle |
| Voice Skills | Layer 4: Skills Layer | SKILL.md files |
| Voice Processing | Layer 3: Hot Path | Python + Deepgram + Hume AI |
| Call Records | Layer 2: Cold Path | PostgreSQL + S3 |
| Telephony Infrastructure | Layer 1: Infrastructure | Twilio + Redis Streams |

### Execution Path Classification

| Skill | Path | Reasoning |
|-------|------|-----------|
| SKILL-109 (Transcription) | **Hot** | Real-time WebSocket streaming ASR |
| SKILL-110 (Voicemail) | **Hybrid** | Async batch processing + notifications |
| SKILL-111 (Sentiment) | **Hot** | Real-time emotion detection (<500ms) |
| SKILL-113 (Multi-Language) | **Hot** | Real-time language detection/switching |
| SKILL-114 (Campaigns) | **Hybrid** | Rules engine + async execution |
| SKILL-115 (IVR Builder) | **Cold** | Configuration management |

### MCP Server Requirements

```yaml
mcp_servers:
  # Voice Processing
  - mcp://voice/transcribe          # Real-time ASR
  - mcp://voice/analyze-sentiment   # Emotion detection
  - mcp://voice/outbound-call       # Campaign execution
  - mcp://voice/ivr-route           # IVR flow execution
  
  # Communication
  - mcp://communication/send        # Multi-channel notifications
  - mcp://communication/voicemail   # Voicemail processing
  
  # Telephony
  - mcp://twilio/call-control       # Call management
  - mcp://twilio/campaign           # Outbound campaigns
  
  # Compliance
  - mcp://compliance/tcpa           # TCPA validation
  - mcp://compliance/consent        # Consent management
```

### Infrastructure Alignment Verification

| Research Spec | Citadel OS Architecture | Status |
|---------------|------------------------|--------|
| Python 3.11+ (FastAPI) | ✅ Aligned | Hot Path services |
| Deepgram Nova-3 | ✅ Aligned | Voice AI provider |
| Hume AI EVI | ✅ Aligned | Emotion detection |
| Twilio Voice | ✅ Aligned | Telephony platform |
| PostgreSQL | ✅ Aligned | Primary database |
| Redis Streams | ✅ Aligned | Event processing |
| S3 | ✅ Aligned | Audio storage |
| ECS/Fargate | ⚠️ Note | Research mentions K8s Helm, we use ECS |

---

## 📊 SKILL SPECIFICATIONS

### SKILL-109: Call Recording Transcription

#### Purpose
Real-time automatic speech recognition (ASR) system with speaker diarization, PII redaction, and searchable archives. Achieves <300ms latency with 53.4% lower WER than competitors.

#### Technical Architecture
```python
from fastapi import FastAPI, WebSocket
from deepgram import DeepgramClient, LiveOptions
from typing import AsyncGenerator
import asyncio

class CallTranscriptionService:
    """
    Real-time call transcription with Deepgram Nova-3.
    Achieves <300ms latency, 95% accuracy for clear English.
    """
    
    def __init__(self):
        self.deepgram = DeepgramClient()
        self.fallback_engine = WhisperFallback()
    
    async def stream_transcription(
        self,
        websocket: WebSocket,
        call_sid: str,
        language: str = "en-US"
    ) -> AsyncGenerator[TranscriptSegment, None]:
        """Stream real-time transcription with speaker diarization."""
        
        options = LiveOptions(
            model="nova-3",
            language=language,
            smart_format=True,
            diarize=True,
            punctuate=True,
            interim_results=True,
            utterance_end_ms=1000,
            vad_events=True,
            # Domain-specific keyterm prompting
            keywords=[
                "check-in:2", "check-out:2", "reservation:2",
                "property:2", "booking:2", "guest:2"
            ]
        )
        
        connection = await self.deepgram.listen.asynclive.v("1").start(options)
        
        try:
            async for audio_chunk in websocket.iter_bytes():
                await connection.send(audio_chunk)
                
                # Process interim results
                result = await connection.receive()
                if result.is_final:
                    segment = self._process_segment(result, call_sid)
                    
                    # PII redaction
                    segment = await self._redact_pii(segment)
                    
                    yield segment
        except Exception as e:
            # Fallback to Whisper on Deepgram failure
            async for segment in self.fallback_engine.transcribe(websocket):
                yield segment
        finally:
            await connection.finish()
    
    async def _redact_pii(self, segment: TranscriptSegment) -> TranscriptSegment:
        """Redact credit cards, SSNs, and sensitive data."""
        
        pii_patterns = {
            'credit_card': r'\b\d{4}[\s-]?\d{4}[\s-]?\d{4}[\s-]?\d{4}\b',
            'ssn': r'\b\d{3}-\d{2}-\d{4}\b',
            'phone': r'\b\d{3}[-.]?\d{3}[-.]?\d{4}\b'
        }
        
        redacted_text = segment.text
        for pii_type, pattern in pii_patterns.items():
            redacted_text = re.sub(pattern, f'[{pii_type.upper()}_REDACTED]', redacted_text)
        
        return TranscriptSegment(
            speaker=segment.speaker,
            text=redacted_text,
            start_time=segment.start_time,
            end_time=segment.end_time,
            confidence=segment.confidence,
            pii_redacted=True
        )
    
    def _process_segment(self, result, call_sid: str) -> TranscriptSegment:
        """Process Deepgram result into standardized segment."""
        
        channel = result.channel
        alternative = channel.alternatives[0]
        
        return TranscriptSegment(
            call_sid=call_sid,
            speaker=self._identify_speaker(result),
            text=alternative.transcript,
            start_time=result.start,
            end_time=result.start + result.duration,
            confidence=alternative.confidence,
            words=[Word(
                text=w.word,
                start=w.start,
                end=w.end,
                confidence=w.confidence
            ) for w in alternative.words]
        )
```

#### Performance Specifications
| Metric | Target | Measurement |
|--------|--------|-------------|
| Latency | <300ms | Real-time monitoring |
| Accuracy (clear English) | 95% | Weekly WER benchmarks |
| Accuracy (accented) | 88-92% | Language-specific testing |
| Concurrent streams | 10,000 | Load testing |

#### Output Schema
```json
{
  "transcript_segment": {
    "call_sid": "CA1234567890",
    "segment_id": "uuid",
    "speaker": "guest",
    "text": "I'd like to check in early tomorrow",
    "start_time": 1.234,
    "end_time": 3.567,
    "confidence": 0.97,
    "language": "en-US",
    "pii_redacted": false,
    "words": [
      {"text": "I'd", "start": 1.234, "end": 1.456, "confidence": 0.98},
      {"text": "like", "start": 1.478, "end": 1.654, "confidence": 0.99}
    ]
  }
}
```

---

### SKILL-110: Voicemail Intelligence

#### Purpose
Automated voicemail transcription with urgency detection and intelligent routing to SMS/email notifications. Converts async voicemail into actionable text notifications with priority routing.

#### Technical Architecture
```python
from celery import Celery
from enum import Enum

class UrgencyLevel(Enum):
    LOW = "low"
    MEDIUM = "medium"
    HIGH = "high"
    CRITICAL = "critical"

class VoicemailIntelligenceService:
    """
    Voicemail processing with urgency detection and routing.
    Integrates with notification system for multi-channel delivery.
    """
    
    def __init__(self):
        self.transcription_service = CallTranscriptionService()
        self.sentiment_service = SentimentAnalysisService()
        self.notification_service = NotificationService()
    
    async def process_voicemail(
        self,
        voicemail_id: str,
        audio_url: str,
        property_id: str
    ) -> VoicemailAnalysis:
        """Process voicemail with urgency detection."""
        
        # Download and transcribe
        audio_data = await self._download_audio(audio_url)
        transcript = await self.transcription_service.batch_transcribe(audio_data)
        
        # Analyze sentiment and urgency
        sentiment = await self.sentiment_service.analyze(transcript.text)
        urgency = self._classify_urgency(transcript.text, sentiment)
        
        # Extract key information
        entities = await self._extract_entities(transcript.text)
        
        analysis = VoicemailAnalysis(
            voicemail_id=voicemail_id,
            property_id=property_id,
            transcript=transcript.text,
            duration=transcript.duration,
            urgency=urgency,
            sentiment=sentiment,
            entities=entities,
            summary=await self._generate_summary(transcript.text),
            processed_at=datetime.utcnow()
        )
        
        # Route notification based on urgency
        await self._route_notification(analysis)
        
        return analysis
    
    def _classify_urgency(
        self,
        text: str,
        sentiment: SentimentScore
    ) -> UrgencyLevel:
        """Classify urgency based on content and sentiment."""
        
        # Emergency keywords (highest priority)
        emergency_keywords = [
            "emergency", "urgent", "fire", "flood", "leak",
            "locked out", "break-in", "police", "ambulance"
        ]
        
        text_lower = text.lower()
        
        # Check for emergency keywords
        if any(kw in text_lower for kw in emergency_keywords):
            return UrgencyLevel.CRITICAL
        
        # High urgency: negative sentiment + urgency indicators
        if sentiment.urgency > 0.7 or sentiment.anger > 0.6:
            return UrgencyLevel.HIGH
        
        # Medium urgency: request or complaint
        request_keywords = ["problem", "issue", "broken", "not working", "complaint"]
        if any(kw in text_lower for kw in request_keywords):
            return UrgencyLevel.MEDIUM
        
        return UrgencyLevel.LOW
    
    async def _route_notification(self, analysis: VoicemailAnalysis):
        """Route notification based on urgency level."""
        
        routing_config = {
            UrgencyLevel.CRITICAL: {
                "channels": ["sms", "push", "call"],
                "recipients": ["on_call_manager", "property_manager"],
                "delay": 0
            },
            UrgencyLevel.HIGH: {
                "channels": ["sms", "push", "email"],
                "recipients": ["property_manager"],
                "delay": 0
            },
            UrgencyLevel.MEDIUM: {
                "channels": ["push", "email"],
                "recipients": ["property_manager"],
                "delay": 300  # 5 minutes
            },
            UrgencyLevel.LOW: {
                "channels": ["email"],
                "recipients": ["property_manager"],
                "delay": 3600  # 1 hour batch
            }
        }
        
        config = routing_config[analysis.urgency]
        
        for channel in config["channels"]:
            await self.notification_service.send(
                channel=channel,
                recipients=config["recipients"],
                template="voicemail_notification",
                data={
                    "property_id": analysis.property_id,
                    "urgency": analysis.urgency.value,
                    "summary": analysis.summary,
                    "transcript": analysis.transcript,
                    "audio_url": analysis.audio_url
                },
                delay=config["delay"]
            )
```

#### Notification Routing Matrix
| Urgency | SMS | Push | Email | Call | Delay |
|---------|-----|------|-------|------|-------|
| Critical | ✅ | ✅ | ❌ | ✅ | 0 |
| High | ✅ | ✅ | ✅ | ❌ | 0 |
| Medium | ❌ | ✅ | ✅ | ❌ | 5 min |
| Low | ❌ | ❌ | ✅ | ❌ | 1 hour |

---

### SKILL-111: Voice Sentiment Analysis

#### Purpose
Real-time emotion detection analyzing tone, pitch, and pace to identify happiness, frustration, or urgency. Provides automatic escalation triggers for negative sentiment with 85% accuracy correlation.

#### Technical Architecture
```python
from hume import HumeClient
from dataclasses import dataclass
from typing import Dict, List

@dataclass
class EmotionProfile:
    anger: float
    frustration: float
    happiness: float
    urgency: float
    confidence: float
    prosody: Dict[str, float]  # pitch, pace, volume

class VoiceSentimentService:
    """
    Real-time emotion detection with Hume AI EVI.
    48+ emotion dimensions with <500ms analysis latency.
    """
    
    def __init__(self):
        self.hume_client = HumeClient()
        self.escalation_thresholds = {
            "anger": 0.8,
            "frustration": 0.7,
            "urgency": 0.9
        }
    
    async def analyze_realtime(
        self,
        audio_stream: WebSocket,
        call_sid: str
    ) -> AsyncGenerator[EmotionProfile, None]:
        """Real-time emotion analysis with escalation triggers."""
        
        async with self.hume_client.connect() as connection:
            async for audio_chunk in audio_stream.iter_bytes():
                # Analyze prosody features
                prosody = self._extract_prosody(audio_chunk)
                
                # Get emotion predictions from Hume AI
                emotions = await connection.send_audio(audio_chunk)
                
                profile = EmotionProfile(
                    anger=emotions.get("anger", 0),
                    frustration=emotions.get("frustration", 0),
                    happiness=emotions.get("happiness", 0),
                    urgency=emotions.get("urgency", 0),
                    confidence=emotions.get("confidence", 0),
                    prosody=prosody
                )
                
                # Check escalation triggers
                escalation = self._evaluate_escalation(profile)
                if escalation:
                    await self._trigger_escalation(call_sid, escalation, profile)
                
                yield profile
    
    def _evaluate_escalation(self, profile: EmotionProfile) -> Optional[EscalationDecision]:
        """Evaluate if escalation is needed based on emotion profile."""
        
        if profile.confidence < 0.85:
            return None  # Low confidence, don't escalate
        
        # Critical: Emergency detection
        if profile.urgency > 0.9:
            return EscalationDecision(
                should_escalate=True,
                escalation_type="emergency",
                reason="Extreme urgency detected",
                priority="critical"
            )
        
        # High: Anger above threshold
        if profile.anger > self.escalation_thresholds["anger"]:
            return EscalationDecision(
                should_escalate=True,
                escalation_type="supervisor",
                reason=f"Anger score {profile.anger:.2f} above threshold",
                priority="high"
            )
        
        # Medium: Frustration above threshold
        if profile.frustration > self.escalation_thresholds["frustration"]:
            return EscalationDecision(
                should_escalate=True,
                escalation_type="agent",
                reason=f"Frustration score {profile.frustration:.2f} above threshold",
                priority="medium"
            )
        
        return None
    
    async def _trigger_escalation(
        self,
        call_sid: str,
        decision: EscalationDecision,
        profile: EmotionProfile
    ):
        """Trigger escalation workflow."""
        
        event = EscalationEvent(
            call_sid=call_sid,
            decision=decision,
            emotion_profile=profile,
            timestamp=datetime.utcnow()
        )
        
        # Publish to Redis Streams for routing
        await self.redis.xadd(
            "voice:escalations",
            event.to_dict()
        )
        
        # Notify supervisor dashboard
        await self.websocket_manager.broadcast(
            channel=f"supervisor:{decision.escalation_type}",
            message=event.to_json()
        )
```

#### Emotion Detection Framework
| Emotion | Threshold | Action | Response Time |
|---------|-----------|--------|---------------|
| Anger >0.8 | High | Immediate escalation | <30 seconds |
| Frustration >0.7 | Medium | Priority queue | <60 seconds |
| Urgency >0.9 | Critical | Emergency protocol | <15 seconds |
| Multiple negative | Combined | Supervisor notification | <45 seconds |

---

### SKILL-113: Multi-Language Voice

#### Purpose
Voice agents supporting English, Spanish, German, Hindi, Portuguese, and 100+ languages with sub-500ms latency optimization and real-time code-switching handling.

#### Technical Architecture
```python
from deepgram import DeepgramClient
from typing import Tuple

class MultiLanguageVoiceService:
    """
    Multi-language voice processing with code-switching.
    100+ languages with sub-500ms latency.
    """
    
    SUPPORTED_LANGUAGES = {
        "en-US": {"model": "nova-3", "voice": "aura-asteria-en"},
        "es-ES": {"model": "nova-3-es", "voice": "aura-stella-es"},
        "pt-BR": {"model": "nova-3-pt", "voice": "aura-luna-pt"},
        "de-DE": {"model": "nova-3-de", "voice": "aura-helena-de"},
        "fr-FR": {"model": "nova-3-fr", "voice": "aura-amélie-fr"},
        "hi-IN": {"model": "nova-3-hi", "voice": "aura-drishti-hi"},
        # ... 100+ more languages
    }
    
    def __init__(self):
        self.deepgram = DeepgramClient()
        self.language_detector = LanguageDetector()
        self.tts_service = TTSService()
    
    async def detect_language(
        self,
        audio_chunk: bytes,
        confidence_threshold: float = 0.95
    ) -> Tuple[str, float]:
        """Detect language from audio with confidence scoring."""
        
        # Use first 2-3 seconds for detection
        result = await self.deepgram.listen.asyncprerecorded.v("1").transcribe_audio(
            audio_chunk,
            options={
                "detect_language": True,
                "model": "nova-3"
            }
        )
        
        detected_language = result.results.channels[0].detected_language
        confidence = result.results.channels[0].language_confidence
        
        if confidence < confidence_threshold:
            # Fallback to user preference or default
            return await self._get_fallback_language()
        
        return detected_language, confidence
    
    async def handle_code_switching(
        self,
        audio_stream: WebSocket,
        initial_language: str
    ) -> AsyncGenerator[TranscriptSegment, None]:
        """Handle mid-conversation language switches."""
        
        current_language = initial_language
        
        # Use Nova-3 "multi" mode for unified multilingual processing
        options = LiveOptions(
            model="nova-3",
            language="multi",  # Unified multilingual mode
            diarize=True,
            smart_format=True,
            punctuate=True
        )
        
        connection = await self.deepgram.listen.asynclive.v("1").start(options)
        
        async for audio_chunk in audio_stream.iter_bytes():
            await connection.send(audio_chunk)
            
            result = await connection.receive()
            if result.is_final:
                detected_lang = result.detected_language
                
                # Handle language switch
                if detected_lang != current_language:
                    await self._handle_language_switch(
                        current_language,
                        detected_lang
                    )
                    current_language = detected_lang
                
                yield TranscriptSegment(
                    text=result.transcript,
                    language=detected_lang,
                    is_code_switch=(detected_lang != initial_language)
                )
    
    async def synthesize_response(
        self,
        text: str,
        language: str,
        emotion_context: Optional[EmotionProfile] = None
    ) -> bytes:
        """Generate TTS response with cultural context."""
        
        config = self.SUPPORTED_LANGUAGES.get(language, self.SUPPORTED_LANGUAGES["en-US"])
        
        # Apply cultural adaptations
        adapted_text = await self._apply_cultural_context(text, language)
        
        # Generate speech with emotion-aware prosody
        audio = await self.tts_service.synthesize(
            text=adapted_text,
            voice=config["voice"],
            emotion=emotion_context
        )
        
        return audio
```

#### Language Support Matrix
| Language | Code | Model | TTS Voice | WER Target |
|----------|------|-------|-----------|------------|
| English (US) | en-US | nova-3 | aura-asteria-en | <5% |
| Spanish (ES) | es-ES | nova-3-es | aura-stella-es | <8% |
| Portuguese (BR) | pt-BR | nova-3-pt | aura-luna-pt | <8% |
| German | de-DE | nova-3-de | aura-helena-de | <8% |
| French | fr-FR | nova-3-fr | aura-amélie-fr | <8% |
| Hindi | hi-IN | nova-3-hi | aura-drishti-hi | <12% |

---

### SKILL-114: Outbound Calling Campaigns

#### Purpose
TCPA-compliant outbound calling system with timezone awareness, Do Not Call (DNC) list management, consent verification, and intelligent voicemail detection.

#### Technical Architecture
```python
from datetime import datetime, time
from typing import List
from pytz import timezone

class OutboundCampaignService:
    """
    TCPA-compliant outbound calling campaigns.
    Zero tolerance for regulatory violations.
    """
    
    # TCPA Quiet Hours (FCC regulation)
    TCPA_QUIET_HOURS = {
        "start": time(21, 0),  # 9 PM local
        "end": time(8, 0)      # 8 AM local
    }
    
    def __init__(self):
        self.twilio = TwilioClient()
        self.dnc_registry = DNCRegistryClient()
        self.consent_manager = ConsentManager()
    
    async def validate_compliance(
        self,
        contact: ContactRecord
    ) -> ComplianceResult:
        """Validate TCPA compliance before initiating call."""
        
        violations = []
        
        # 1. Check consent (one-to-one requirement as of Jan 2025)
        consent = await self.consent_manager.verify(
            phone=contact.phone,
            campaign_type=contact.campaign_type
        )
        if not consent.is_valid:
            violations.append(ComplianceViolation(
                type="consent",
                message="Express written consent required",
                severity="critical"
            ))
        
        # 2. Check DNC registry (National + State)
        dnc_status = await self.dnc_registry.check(contact.phone)
        if dnc_status.on_list:
            violations.append(ComplianceViolation(
                type="dnc",
                message=f"Number on {dnc_status.list_type} DNC registry",
                severity="critical"
            ))
        
        # 3. Check timezone compliance
        if not self._is_within_calling_hours(contact.phone):
            violations.append(ComplianceViolation(
                type="timezone",
                message="Outside TCPA permitted hours (8am-9pm local)",
                severity="critical"
            ))
        
        # 4. Check frequency limits (max 2 calls/24h)
        recent_calls = await self._get_recent_calls(contact.phone, hours=24)
        if len(recent_calls) >= 2:
            violations.append(ComplianceViolation(
                type="frequency",
                message="Exceeded maximum 2 calls per 24-hour period",
                severity="high"
            ))
        
        return ComplianceResult(
            is_compliant=len(violations) == 0,
            violations=violations,
            checked_at=datetime.utcnow()
        )
    
    def _is_within_calling_hours(self, phone: str) -> bool:
        """Check if current time is within TCPA permitted hours."""
        
        # Get timezone from area code
        tz = self._get_timezone_from_phone(phone)
        local_time = datetime.now(tz).time()
        
        # Check quiet hours (9 PM - 8 AM)
        if local_time >= self.TCPA_QUIET_HOURS["start"]:
            return False
        if local_time < self.TCPA_QUIET_HOURS["end"]:
            return False
        
        return True
    
    async def execute_campaign(
        self,
        campaign_id: str,
        contacts: List[ContactRecord]
    ) -> CampaignExecution:
        """Execute outbound campaign with compliance validation."""
        
        results = []
        
        for contact in contacts:
            # Validate compliance before each call
            compliance = await self.validate_compliance(contact)
            
            if not compliance.is_compliant:
                results.append(CallResult(
                    contact_id=contact.id,
                    status="blocked",
                    reason=compliance.violations[0].message
                ))
                continue
            
            # Initiate call with AMD (Answering Machine Detection)
            call = await self.twilio.calls.create(
                to=contact.phone,
                from_=self._get_caller_id(campaign_id),
                url=f"{self.webhook_base}/campaign/{campaign_id}/call",
                machine_detection="DetectMessageEnd",
                machine_detection_timeout=2000  # 2 seconds
            )
            
            results.append(CallResult(
                contact_id=contact.id,
                call_sid=call.sid,
                status="initiated"
            ))
        
        return CampaignExecution(
            campaign_id=campaign_id,
            total_contacts=len(contacts),
            calls_initiated=sum(1 for r in results if r.status == "initiated"),
            calls_blocked=sum(1 for r in results if r.status == "blocked"),
            results=results
        )
    
    async def handle_amd_result(
        self,
        call_sid: str,
        amd_status: str
    ):
        """Handle Answering Machine Detection result."""
        
        if amd_status == "human":
            # Connect to live agent or play personalized message
            await self._connect_live_call(call_sid)
        elif amd_status in ["machine_start", "machine_end_beep"]:
            # Drop pre-recorded voicemail
            await self._drop_voicemail(call_sid)
        else:
            # Unknown/fax - end call
            await self.twilio.calls(call_sid).update(status="completed")
```

#### TCPA Compliance Checklist
| Requirement | Implementation | Validation |
|-------------|----------------|------------|
| Express Written Consent | Consent manager with audit trail | Real-time verification |
| One-to-One Consent (Jan 2025) | Specific consent per campaign type | Database enforcement |
| DNC Registry Check | National + State registry integration | Pre-call validation |
| Timezone Compliance | Area code → timezone mapping | 8 AM - 9 PM local only |
| Frequency Limits | Call history tracking | Max 2 calls/24 hours |
| Caller ID | Valid, non-spoofed caller ID | Twilio verification |

---

### SKILL-115: IVR Flow Builder

#### Purpose
Visual drag-and-drop interface for designing call routing flows with A/B testing framework, emergency bypass, and performance analytics.

#### Technical Architecture
```python
from dataclasses import dataclass
from typing import List, Dict, Optional
from enum import Enum

class NodeType(Enum):
    START = "start"
    MENU = "menu"
    INPUT = "input"
    CONDITION = "condition"
    ACTION = "action"
    TRANSFER = "transfer"
    VOICEMAIL = "voicemail"
    END = "end"

@dataclass
class IVRNode:
    id: str
    type: NodeType
    config: Dict
    next_nodes: List[str]

class IVRFlowBuilderService:
    """
    Visual IVR flow builder with A/B testing.
    Non-technical staff can design call flows.
    """
    
    def __init__(self):
        self.flow_repository = FlowRepository()
        self.twilio = TwilioClient()
    
    def validate_flow(self, flow: IVRFlow) -> ValidationResult:
        """Validate IVR flow for completeness and correctness."""
        
        errors = []
        warnings = []
        
        # Check for start node
        start_nodes = [n for n in flow.nodes if n.type == NodeType.START]
        if len(start_nodes) != 1:
            errors.append("Flow must have exactly one start node")
        
        # Check for dead ends
        for node in flow.nodes:
            if node.type not in [NodeType.END, NodeType.VOICEMAIL, NodeType.TRANSFER]:
                if not node.next_nodes:
                    errors.append(f"Node {node.id} has no outgoing connections")
        
        # Check for unreachable nodes
        reachable = self._find_reachable_nodes(flow, start_nodes[0].id)
        unreachable = [n for n in flow.nodes if n.id not in reachable]
        for node in unreachable:
            warnings.append(f"Node {node.id} is unreachable")
        
        # Check emergency bypass exists
        emergency_nodes = [n for n in flow.nodes if n.config.get("emergency_bypass")]
        if not emergency_nodes:
            warnings.append("No emergency bypass configured (recommended)")
        
        return ValidationResult(
            is_valid=len(errors) == 0,
            errors=errors,
            warnings=warnings
        )
    
    def compile_to_twiml(self, flow: IVRFlow) -> str:
        """Compile visual flow to TwiML for Twilio execution."""
        
        twiml_segments = {}
        
        for node in flow.nodes:
            twiml = self._node_to_twiml(node, flow)
            twiml_segments[node.id] = twiml
        
        return self._combine_twiml(twiml_segments, flow)
    
    def _node_to_twiml(self, node: IVRNode, flow: IVRFlow) -> str:
        """Convert single node to TwiML."""
        
        if node.type == NodeType.MENU:
            return self._menu_to_twiml(node)
        elif node.type == NodeType.INPUT:
            return self._input_to_twiml(node)
        elif node.type == NodeType.TRANSFER:
            return self._transfer_to_twiml(node)
        elif node.type == NodeType.CONDITION:
            return self._condition_to_twiml(node, flow)
        # ... other node types
    
    def _menu_to_twiml(self, node: IVRNode) -> str:
        """Generate TwiML for menu node."""
        
        options = node.config.get("options", [])
        prompt = node.config.get("prompt", "Please select an option")
        
        twiml = f"""
        <Gather numDigits="1" action="/ivr/menu/{node.id}" timeout="5">
            <Say voice="Polly.Joanna">{prompt}</Say>
            {''.join([f'<Say>Press {opt["digit"]} for {opt["label"]}</Say>' for opt in options])}
        </Gather>
        <Say>We didn't receive any input. Goodbye!</Say>
        """
        
        return twiml
    
    async def run_ab_test(
        self,
        flow_a: str,
        flow_b: str,
        traffic_split: float = 0.5,
        duration_days: int = 7
    ) -> ABTestResult:
        """Run A/B test between two flow versions."""
        
        test = ABTest(
            flow_a_id=flow_a,
            flow_b_id=flow_b,
            traffic_split=traffic_split,
            start_date=datetime.utcnow(),
            end_date=datetime.utcnow() + timedelta(days=duration_days)
        )
        
        await self.flow_repository.save_ab_test(test)
        
        return ABTestResult(
            test_id=test.id,
            status="running",
            metrics_url=f"/ivr/ab-test/{test.id}/metrics"
        )
```

#### IVR Node Types
| Node Type | Purpose | Configuration |
|-----------|---------|---------------|
| Start | Call entry point | Greeting message |
| Menu | Options presentation | DTMF digits, prompts |
| Input | Collect user data | Digit count, timeout |
| Condition | Logic branching | Expression, routes |
| Action | External integration | API call, webhook |
| Transfer | Connect to agent | Queue, direct dial |
| Voicemail | Record message | Max length, transcribe |
| End | Call termination | Goodbye message |

---

## 🗄️ DATABASE SCHEMA

### PostgreSQL Tables

```sql
-- Call Records
CREATE TABLE call_records (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    call_sid VARCHAR(34) NOT NULL UNIQUE,
    from_number VARCHAR(20) NOT NULL,
    to_number VARCHAR(20) NOT NULL,
    direction VARCHAR(10) NOT NULL,  -- 'inbound', 'outbound'
    status VARCHAR(20) NOT NULL,
    duration INTEGER,
    start_time TIMESTAMPTZ NOT NULL,
    end_time TIMESTAMPTZ,
    property_id UUID REFERENCES properties(id),
    transcript JSONB,
    sentiment_scores JSONB,
    language VARCHAR(10),
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

-- Voice Sessions (Redis-backed, schema for reference)
CREATE TABLE voice_sessions (
    session_id UUID PRIMARY KEY,
    call_sid VARCHAR(34) NOT NULL,
    user_id UUID,
    language_code VARCHAR(10) DEFAULT 'en-US',
    sentiment_state JSONB,
    active_flows JSONB,
    created_at TIMESTAMPTZ DEFAULT NOW(),
    expires_at TIMESTAMPTZ
);

-- Campaign Configuration
CREATE TABLE outbound_campaigns (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    property_id UUID REFERENCES properties(id),
    campaign_type VARCHAR(50) NOT NULL,
    status VARCHAR(20) DEFAULT 'draft',
    message_template TEXT,
    voicemail_template TEXT,
    timezone_aware BOOLEAN DEFAULT TRUE,
    max_attempts INTEGER DEFAULT 2,
    consent_required BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMPTZ DEFAULT NOW(),
    scheduled_start TIMESTAMPTZ,
    scheduled_end TIMESTAMPTZ
);

-- Compliance Audit Log (Immutable)
CREATE TABLE compliance_audit_log (
    id BIGSERIAL PRIMARY KEY,
    call_sid VARCHAR(34),
    campaign_id UUID,
    phone_number VARCHAR(20),
    check_type VARCHAR(50) NOT NULL,
    check_result BOOLEAN NOT NULL,
    violation_details JSONB,
    checked_at TIMESTAMPTZ DEFAULT NOW()
);

-- IVR Flows
CREATE TABLE ivr_flows (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    property_id UUID REFERENCES properties(id),
    version INTEGER DEFAULT 1,
    status VARCHAR(20) DEFAULT 'draft',
    flow_definition JSONB NOT NULL,
    compiled_twiml TEXT,
    created_at TIMESTAMPTZ DEFAULT NOW(),
    published_at TIMESTAMPTZ
);

-- Indexes
CREATE INDEX idx_call_records_property ON call_records(property_id, start_time DESC);
CREATE INDEX idx_call_records_sentiment ON call_records USING GIN(sentiment_scores);
CREATE INDEX idx_compliance_audit_phone ON compliance_audit_log(phone_number, checked_at DESC);
CREATE INDEX idx_ivr_flows_property ON ivr_flows(property_id, status);
```

---

## 🔗 INTEGRATION ARCHITECTURE

### External Services

| Service | Purpose | Auth | Rate Limit |
|---------|---------|------|------------|
| Deepgram Nova-3 | ASR engine | API Key | 10,000 concurrent |
| Hume AI EVI | Emotion detection | API Key | 5,000/min |
| Twilio Voice | Telephony | Account SID + Auth Token | Per account |
| DNC Registry | Compliance | API Key | 10,000/day |

### Real-Time Voice Pipeline

```
┌────────────────────────────────────────────────────────────────────┐
│                    Voice Processing Pipeline                        │
├────────────────────────────────────────────────────────────────────┤
│                                                                     │
│   Call Sources                                                      │
│   ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐            │
│   │ Inbound  │ │ Outbound │ │ Voicemail│ │Emergency │            │
│   │  Calls   │ │ Campaign │ │  Drops   │ │  Bypass  │            │
│   └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘            │
│        │            │            │            │                    │
│        └────────────┼────────────┼────────────┘                    │
│                     │                                              │
│                     ▼                                              │
│   ┌─────────────────────────────────────────────────────────────┐ │
│   │              Twilio Voice Platform                           │ │
│   └────────────────────────────┬────────────────────────────────┘ │
│                                │                                   │
│         ┌──────────────────────┼──────────────────────┐           │
│         │                      │                      │            │
│         ▼                      ▼                      ▼            │
│   ┌──────────┐          ┌──────────┐          ┌──────────┐        │
│   │ Deepgram │          │ Hume AI  │          │ Language │        │
│   │  Nova-3  │          │   EVI    │          │ Detection│        │
│   │   ASR    │          │ Emotion  │          │          │        │
│   └────┬─────┘          └────┬─────┘          └────┬─────┘        │
│        │                     │                     │               │
│        └─────────────────────┼─────────────────────┘               │
│                              │                                     │
│                              ▼                                     │
│   ┌─────────────────────────────────────────────────────────────┐ │
│   │              Redis Streams (Event Processing)                │ │
│   └────────────────────────────┬────────────────────────────────┘ │
│                                │                                   │
│         ┌──────────────────────┼──────────────────────┐           │
│         │                      │                      │            │
│         ▼                      ▼                      ▼            │
│   ┌──────────┐          ┌──────────┐          ┌──────────┐        │
│   │PostgreSQL│          │    S3    │          │ClickHouse│        │
│   │  (Calls) │          │ (Audio)  │          │(Analytics)│       │
│   └──────────┘          └──────────┘          └──────────┘        │
│                                                                     │
└────────────────────────────────────────────────────────────────────┘
```

---

## 📊 PERFORMANCE REQUIREMENTS

| Skill | Response Time | Throughput | Availability |
|-------|--------------|------------|--------------|
| SKILL-109 (Transcription) | <300ms | 10,000 concurrent | 99.9% |
| SKILL-110 (Voicemail) | <5s (async) | 1,000/min | 99.5% |
| SKILL-111 (Sentiment) | <500ms | 5,000/min | 99.5% |
| SKILL-113 (Multi-Language) | <2s detection | 10,000 concurrent | 99.9% |
| SKILL-114 (Campaigns) | <2s initiation | 50,000/hour | 99.9% |
| SKILL-115 (IVR) | <1s response | 1,000 concurrent | 99.9% |

---

## 🧪 TESTING STRATEGY

### Unit Tests
- ASR accuracy validation
- Sentiment scoring algorithms
- TCPA compliance rules
- IVR flow compilation

### Integration Tests
- Deepgram API connectivity
- Hume AI emotion detection
- Twilio call handling
- DNC registry validation

### Performance Tests
- 10,000 concurrent transcription streams
- Campaign execution throughput
- IVR response latency

### Compliance Tests
- TCPA validation scenarios
- Consent verification
- DNC list enforcement
- Timezone compliance

---

## 🔐 SECURITY CONSIDERATIONS

### Data Protection
- End-to-end encryption (TLS 1.3 + AES-256)
- PII redaction before storage
- Encrypted audio at rest (S3 SSE-KMS)
- Access controls (RBAC)

### Compliance
- TCPA: Zero tolerance for violations
- GDPR: Data retention policies
- SOC 2: Audit logging
- Call recording consent

### Access Control
| Role | Voice Data | Campaigns | Compliance Logs |
|------|------------|-----------|-----------------|
| Voice Agent | Read transcripts | None | None |
| Operations Manager | Full access | Execute | Read-only |
| Compliance Officer | Audit access | Review | Full access |
| Administrator | Technical | None | Full access |

---

## 📁 FILE LOCATIONS

```
specs/communication/
└── SPEC-SKILL-109-115-VOICE-COMMUNICATION.md (this file)

knowledge/communication/
└── KD-PHASE2-G4-voice-communication.md (research source)

skills/communication/
├── SKILL-109-call-transcription.md
├── SKILL-110-voicemail-intelligence.md
├── SKILL-111-voice-sentiment.md
├── SKILL-113-multi-language-voice.md
├── SKILL-114-outbound-campaigns.md
└── SKILL-115-ivr-flow-builder.md
```

---

## 🚀 IMPLEMENTATION ROADMAP

| Week | Milestone |
|------|-----------|
| 1-2 | SKILL-109 (Transcription) + Infrastructure |
| 3-4 | SKILL-111 (Sentiment) + SKILL-113 (Multi-Language) |
| 5-6 | SKILL-114 (Campaigns) + Compliance Engine |
| 7-8 | SKILL-110 (Voicemail) + SKILL-115 (IVR Builder) |

---

**Status**: ✅ SPECIFIED - Ready for Engineering Implementation

