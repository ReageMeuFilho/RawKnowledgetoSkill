# Skill Specification: Hospitality Premium Platform

> **Skills Covered**: SKILL-087, SKILL-124, SKILL-125, SKILL-126, SKILL-127, SKILL-055
> **Category**: Hospitality / Premium Features
> **Phase**: Phase 2 - Group 7 (Hospitality Premium)
> **Priority**: P2 (Enhanced)
> **Status**: SPECIFIED
> **Last Updated**: January 2026
> **Research Source**: Research Phase 2 Group 7.txt (~9,259 lines)

---

## 📋 EXECUTIVE SUMMARY

The Hospitality Premium Platform delivers **6 hotel-grade skills** that transform short-term rental operations into premium hospitality experiences:

- **25-40% TRevPAR increase** through dynamic upgrades and upselling
- **360% upsell revenue growth** (Hard Rock Hotel case study)
- **24% operational efficiency improvement**
- **>4.5/5.0 guest satisfaction scores**
- **15-25% direct booking increase** via SEO optimization

### Skills Overview

| Skill ID | Name | Category | Description |
|----------|------|----------|-------------|
| **SKILL-087** | Front Desk Command Center | Operations | Real-time Tetris-style dashboard |
| **SKILL-124** | Digital Concierge | Guest Experience | GPT-4 powered recommendations |
| **SKILL-125** | Experience Booking | Revenue | Viator/GetYourGuide integration |
| **SKILL-126** | Room Upgrade Management | Revenue | Dynamic upgrade pricing |
| **SKILL-127** | Early Check-in/Late Checkout | Operations | Smart lock flexible access |
| **SKILL-055** | Website SEO | Marketing | VacationRental schema implementation |

---

## 🏗️ ARCHITECTURE ALIGNMENT NOTES

### Layer Mapping (Citadel OS 6-Layer Stack)

| Component | Citadel OS Layer | Implementation |
|-----------|------------------|----------------|
| Guest Dashboards | Layer 6: Applications | React 19 + TypeScript |
| Hospitality Bundle | Layer 5: Domain Bundles | Premium hospitality bundle |
| Premium Skills | Layer 4: Skills Layer | SKILL.md files |
| Real-time Engine | Layer 3: Hot Path | FastAPI + WebSocket |
| Pricing Engine | Layer 2: Cold Path | Python algorithms |
| Data Infrastructure | Layer 1: Infrastructure | MongoDB + Redis |

### Execution Path Classification

| Skill | Path | Reasoning |
|-------|------|-----------|
| SKILL-087 (Front Desk) | **Hot** | Real-time WebSocket (<2s) |
| SKILL-124 (Concierge) | **Hybrid** | GPT-4 AI + caching |
| SKILL-125 (Experience) | **Cold** | Third-party API booking |
| SKILL-126 (Upgrades) | **Hybrid** | ML pricing + real-time offers |
| SKILL-127 (Flex Access) | **Hot** | Smart lock real-time control |
| SKILL-055 (SEO) | **Cold** | Static generation + CDN |

### MCP Server Requirements

```yaml
mcp_servers:
  # Front Desk Command Center
  - mcp://hospitality/front-desk        # Dashboard operations
  - mcp://hospitality/room-status       # Real-time room updates
  
  # Digital Concierge
  - mcp://ai/concierge-recommend        # GPT-4 recommendations
  - mcp://integration/google-places     # Local business data
  
  # Experience Booking
  - mcp://integration/viator            # Viator API
  - mcp://integration/getyourguide      # GetYourGuide API
  - mcp://treasury-write                # Commission tracking
  
  # Room Upgrades
  - mcp://pricing/upgrade-engine        # Dynamic pricing
  - mcp://inventory/protection          # Inventory management
  
  # Flexible Access
  - mcp://integration/smart-lock        # Lock control
  - mcp://temporal-trigger              # Scheduled access codes
  
  # Website SEO
  - mcp://content/schema-generator      # Schema.org markup
  - mcp://integration/search-console    # Google integration
```

### Infrastructure Alignment Verification

| Research Spec | Citadel OS Architecture | Status |
|---------------|------------------------|--------|
| React 19 | ✅ Aligned | Frontend framework |
| Next.js 15 | ✅ Aligned | SSR/SSG for SEO |
| Python 3.12+ | ✅ Aligned | Backend services |
| FastAPI | ✅ Aligned | High-performance APIs |
| MongoDB | ⚠️ Adjustment | Use DocumentDB on AWS |
| Redis 7.2+ | ✅ Aligned | Caching layer |
| Socket.IO | ✅ Aligned | WebSocket management |
| OpenAI GPT-4 | ✅ Aligned | AI recommendations |
| AWS ECS/Fargate | ✅ Aligned | Container orchestration |

---

## 📊 SKILL SPECIFICATIONS

### SKILL-087: Front Desk Command Center

#### Purpose
Hotel-grade front desk dashboard with "Tetris-style" timeline visualization enabling real-time room management, guest operations, and housekeeping coordination.

#### Technical Architecture
```typescript
// Front Desk Dashboard Service
interface FrontDeskDashboard {
  timeline: TimelineView;
  guestLookup: GuestSearchService;
  roomManagement: RoomStatusManager;
  walkInBooking: WalkInProcessor;
  notifications: RealTimeNotifications;
}

interface TimelineView {
  propertyId: string;
  dateRange: DateRange;
  rooms: RoomOccupancy[];
  arrivals: GuestArrival[];
  departures: GuestDeparture[];
  housekeeping: HousekeepingStatus[];
}

interface RoomOccupancy {
  roomId: string;
  roomNumber: string;
  roomType: string;
  status: 'available' | 'occupied' | 'dirty' | 'cleaning' | 'maintenance' | 'ooo';
  currentGuest?: {
    guestId: string;
    name: string;
    checkInDate: Date;
    checkOutDate: Date;
    vipStatus?: string;
  };
  housekeeping: {
    lastCleaned: Date;
    assignedStaff?: string;
    estimatedCompletion?: Date;
  };
}

// WebSocket Real-time Updates
class FrontDeskWebSocket {
  private io: Server;
  
  constructor() {
    this.io = new Server({
      cors: { origin: process.env.FRONTEND_URL },
      transports: ['websocket', 'polling']
    });
  }
  
  emitRoomStatusUpdate(propertyId: string, roomStatus: RoomOccupancy): void {
    this.io.to(`property:${propertyId}`).emit('room_status_update', roomStatus);
  }
  
  emitGuestArrival(propertyId: string, arrival: GuestArrival): void {
    this.io.to(`property:${propertyId}`).emit('guest_arrival', arrival);
  }
  
  emitHousekeepingComplete(propertyId: string, roomId: string): void {
    this.io.to(`property:${propertyId}`).emit('housekeeping_complete', { roomId });
  }
}
```

#### API Endpoints
| Endpoint | Method | Purpose | Response Time |
|----------|--------|---------|---------------|
| `/api/dashboard/timeline` | GET | Retrieve timeline data | <2s |
| `/api/guests/search` | GET | Search guest profiles | <500ms |
| `/api/rooms/status` | GET | Get room statuses | <1s |
| `/api/walkin/create` | POST | Process walk-in | <3s |
| `/api/checkin/process` | POST | Execute check-in | <2s |

#### Performance Requirements
- Dashboard load time: <2 seconds
- Real-time updates: <500ms latency
- Concurrent users: 100+ simultaneous front desk operations
- WebSocket connections: 1000+ per property cluster

---

### SKILL-124: Digital Concierge

#### Purpose
GPT-4 powered AI concierge providing personalized local recommendations based on guest preferences, weather, location, and context.

#### Technical Architecture
```python
from langchain_openai import ChatOpenAI
from langchain.prompts import ChatPromptTemplate
from dataclasses import dataclass
from typing import List, Dict, Optional
import httpx

@dataclass
class Recommendation:
    id: str
    name: str
    category: str  # restaurant, attraction, entertainment, shopping
    description: str
    ai_insight: str
    rating: float
    price_level: int
    distance_km: float
    estimated_time: str
    opening_hours: Dict
    booking_url: Optional[str]
    images: List[str]
    personalized_reason: str
    score: float

@dataclass
class GuestContext:
    guest_id: str
    guest_type: str  # business, leisure, family
    preferences: List[str]
    past_bookings: List[str]
    weather: Dict
    time_of_day: str
    group_size: int
    budget_indicator: str
    special_occasion: Optional[str]


class DigitalConciergeService:
    """
    GPT-4 powered local recommendation engine.
    Achieves 95% recommendation relevance.
    """
    
    def __init__(self):
        self.llm = ChatOpenAI(
            model="gpt-4",
            temperature=0.7,
            max_tokens=500
        )
        self.google_places = GooglePlacesClient()
        self.redis = RedisClient()
    
    async def get_recommendations(
        self,
        property_id: str,
        guest_context: GuestContext,
        query: Optional[str] = None
    ) -> List[Recommendation]:
        """Generate personalized recommendations."""
        
        # Check cache first
        cache_key = f"recommendations:{property_id}:{guest_context.guest_id}"
        cached = await self.redis.get(cache_key)
        if cached and not query:
            return cached
        
        # Get property location
        property_data = await self._get_property(property_id)
        location = property_data['location']
        
        # Fetch local businesses from Google Places
        places = await self.google_places.nearby_search(
            location=location,
            radius=5000,
            types=['restaurant', 'tourist_attraction', 'entertainment']
        )
        
        # Get weather context
        weather = await self._get_weather(location)
        
        # Generate AI-powered recommendations
        prompt = ChatPromptTemplate.from_messages([
            ("system", """You are a local concierge expert providing personalized 
            recommendations for hotel guests. Consider the guest's preferences, 
            weather conditions, and context to provide curated suggestions."""),
            ("user", """
            Guest Profile: {guest_context}
            Weather: {weather}
            Available Places: {places}
            Specific Query: {query}
            
            Provide 5-10 personalized recommendations with insights.""")
        ])
        
        response = await self.llm.ainvoke(
            prompt.format(
                guest_context=guest_context,
                weather=weather,
                places=places[:20],
                query=query or "general recommendations"
            )
        )
        
        # Parse and score recommendations
        recommendations = self._parse_recommendations(response, places)
        scored = self._score_recommendations(recommendations, guest_context)
        
        # Cache results
        await self.redis.setex(cache_key, 1800, scored)  # 30 min cache
        
        return scored[:10]
    
    def _score_recommendations(
        self,
        recommendations: List[Recommendation],
        context: GuestContext
    ) -> List[Recommendation]:
        """Score recommendations using multi-factor algorithm."""
        
        for rec in recommendations:
            # Score = (Relevance × 0.4) + (Quality × 0.3) + 
            #         (Distance × 0.2) + (Availability × 0.1)
            relevance = self._calculate_relevance(rec, context)
            quality = rec.rating / 5.0 * 100
            distance = max(0, 100 - (rec.distance_km * 2))
            availability = 100 if rec.opening_hours.get('open_now') else 50
            
            rec.score = (
                relevance * 0.4 +
                quality * 0.3 +
                distance * 0.2 +
                availability * 0.1
            )
        
        return sorted(recommendations, key=lambda x: x.score, reverse=True)
```

#### Personalization Factors
| Factor | Weight | Data Source | Impact |
|--------|--------|-------------|--------|
| Guest Type | 25% | Profile analysis | Business/leisure filtering |
| Past Preferences | 20% | Booking history | Similar experience matching |
| Weather Conditions | 15% | Weather API | Indoor/outdoor filtering |
| Time of Day | 15% | Current time | Operating hours |
| Group Size | 10% | Booking details | Capacity matching |
| Budget Indicators | 10% | Spending history | Price range filtering |
| Special Occasions | 5% | Calendar/profile | Event-specific |

---

### SKILL-125: Experience Booking

#### Purpose
Integration with Viator and GetYourGuide APIs for seamless experience booking with commission tracking (8-20% affiliate, 20-30% merchant).

#### Technical Architecture
```python
from dataclasses import dataclass
from typing import List, Dict, Optional
from decimal import Decimal
from enum import Enum

class BookingModel(Enum):
    AFFILIATE = "affiliate"  # 8-12% commission, low liability
    MERCHANT = "merchant"    # 20-30% commission, high liability
    DIRECT = "direct"        # 15-20% commission, medium liability

@dataclass
class ExperienceBooking:
    booking_id: str
    provider: str  # viator, getyourguide
    booking_model: BookingModel
    experience: Dict
    guest_id: str
    booking_date: str
    participants: int
    total_price: Decimal
    commission: CommissionDetails
    cancellation_policy: Dict
    status: str

@dataclass
class CommissionDetails:
    rate: Decimal  # 0.08 to 0.30
    amount: Decimal
    processing_fee: Decimal
    net_revenue: Decimal


class ExperienceBookingService:
    """
    Multi-provider experience booking with commission management.
    Supports 300,000+ bookable experiences.
    """
    
    COMMISSION_RATES = {
        'viator': {
            BookingModel.AFFILIATE: Decimal('0.10'),  # 8-12%
            BookingModel.MERCHANT: Decimal('0.22')    # 20-25%
        },
        'getyourguide': {
            BookingModel.AFFILIATE: Decimal('0.08'),  # 8-10%
            BookingModel.MERCHANT: Decimal('0.27')    # 25-30%
        }
    }
    
    PROCESSING_FEES = {
        BookingModel.AFFILIATE: Decimal('0.029'),   # 2.9% + $0.30
        BookingModel.MERCHANT: Decimal('0.035')     # 3.5% + $0.30
    }
    
    def __init__(self):
        self.viator = ViatorClient()
        self.getyourguide = GetYourGuideClient()
        self.payment = StripeClient()
        self.db = MongoDB()
    
    async def search_experiences(
        self,
        location: Dict,
        category: Optional[str] = None,
        date: Optional[str] = None
    ) -> List[Dict]:
        """Search experiences across all providers."""
        
        # Query both providers in parallel
        viator_results, gyg_results = await asyncio.gather(
            self.viator.search(location, category, date),
            self.getyourguide.search(location, category, date)
        )
        
        # Normalize and merge results
        all_results = [
            self._normalize_viator(exp) for exp in viator_results
        ] + [
            self._normalize_gyg(exp) for exp in gyg_results
        ]
        
        # Sort by commission rate (prefer higher commission)
        return sorted(
            all_results,
            key=lambda x: self.COMMISSION_RATES[x['provider']][x['booking_model']],
            reverse=True
        )
    
    async def create_booking(
        self,
        experience_id: str,
        provider: str,
        guest_id: str,
        participants: int,
        payment_method: str
    ) -> ExperienceBooking:
        """Create experience booking with commission tracking."""
        
        # Get experience details
        if provider == 'viator':
            experience = await self.viator.get_experience(experience_id)
            booking_model = BookingModel.AFFILIATE
        else:
            experience = await self.getyourguide.get_experience(experience_id)
            booking_model = BookingModel.AFFILIATE
        
        # Calculate pricing
        total_price = Decimal(str(experience['price'])) * participants
        commission_rate = self.COMMISSION_RATES[provider][booking_model]
        commission_amount = total_price * commission_rate
        processing_fee = (total_price * self.PROCESSING_FEES[booking_model]) + Decimal('0.30')
        net_revenue = commission_amount - processing_fee
        
        # Process payment
        payment = await self.payment.charge(
            amount=total_price,
            payment_method=payment_method,
            metadata={'type': 'experience_booking', 'provider': provider}
        )
        
        # Create booking with provider
        if provider == 'viator':
            provider_booking = await self.viator.create_booking(
                experience_id, participants, payment.id
            )
        else:
            provider_booking = await self.getyourguide.create_booking(
                experience_id, participants, payment.id
            )
        
        # Store booking record
        booking = ExperienceBooking(
            booking_id=str(uuid4()),
            provider=provider,
            booking_model=booking_model,
            experience=experience,
            guest_id=guest_id,
            booking_date=datetime.utcnow().isoformat(),
            participants=participants,
            total_price=total_price,
            commission=CommissionDetails(
                rate=commission_rate,
                amount=commission_amount,
                processing_fee=processing_fee,
                net_revenue=net_revenue
            ),
            cancellation_policy=experience['cancellation_policy'],
            status='confirmed'
        )
        
        await self.db.experience_bookings.insert_one(asdict(booking))
        
        # Track commission in TigerBeetle
        await self._record_commission(booking)
        
        return booking
```

#### Commission Matrix
| Provider | Model | Commission | Liability | Processing Fee |
|----------|-------|------------|-----------|----------------|
| Viator | Affiliate | 8-12% | Low | 2.9% + $0.30 |
| Viator | White-label | 20-25% | High | 3.5% + $0.30 |
| GetYourGuide | Affiliate | 8-10% | Low | 2.9% + $0.30 |
| GetYourGuide | Merchant | 25-30% | High | 3.5% + $0.30 |

---

### SKILL-126: Room Upgrade Management

#### Purpose
Dynamic upgrade pricing engine with demand forecasting, guest segmentation, and inventory protection achieving 25-40% TRevPAR increase.

#### Technical Architecture
```python
from dataclasses import dataclass
from typing import Dict, List, Optional, Tuple
from decimal import Decimal
from datetime import datetime, timedelta

@dataclass
class UpgradeOffer:
    offer_id: str
    guest_id: str
    booking_id: str
    from_room: str
    to_room: str
    original_price: Decimal
    upgrade_price: Decimal
    discount_factor: Decimal
    final_price: Decimal
    offer_sent: datetime
    response_deadline: datetime
    status: str  # pending, accepted, declined, expired
    channel: str  # email, sms, app, front_desk

@dataclass
class GuestSegment:
    segment_id: str
    name: str  # VIP/Loyalty, High Spender, Regular, Price Sensitive, First-time
    value_score_range: Tuple[int, int]
    discount_range: Tuple[Decimal, Decimal]
    offer_timing_days: int
    pricing_strategy: str


class DynamicUpgradePricingEngine:
    """
    ML-powered upgrade pricing with inventory protection.
    Achieves 360% upsell revenue growth (industry benchmark).
    """
    
    SEGMENTS = {
        'vip': GuestSegment('vip', 'VIP/Loyalty', (90, 100), (Decimal('0.6'), Decimal('0.8')), 7, 'premium_experience'),
        'high_spender': GuestSegment('high_spender', 'High Spender', (70, 89), (Decimal('0.7'), Decimal('0.9')), 5, 'value_enhancement'),
        'regular': GuestSegment('regular', 'Regular Guest', (50, 69), (Decimal('0.8'), Decimal('1.0')), 3, 'standard_upgrade'),
        'price_sensitive': GuestSegment('price_sensitive', 'Price Sensitive', (30, 49), (Decimal('0.5'), Decimal('0.7')), 0, 'last_minute_deals'),
        'first_time': GuestSegment('first_time', 'First-time Guest', (0, 29), (Decimal('0.6'), Decimal('0.8')), 0, 'experience_sampling')
    }
    
    def __init__(self):
        self.db = MongoDB()
        self.redis = RedisClient()
        self.demand_forecaster = DemandForecaster()
    
    async def calculate_upgrade_price(
        self,
        property_id: str,
        from_room_type: str,
        to_room_type: str,
        check_in_date: datetime,
        guest_id: str
    ) -> Optional[UpgradeOffer]:
        """
        Calculate dynamic upgrade price.
        
        Formula:
        Upgrade_Price = Base_Upgrade_Rate × Demand_Multiplier × 
                        Guest_Value_Factor × Timing_Discount × 
                        Inventory_Adjustment
        """
        
        # Check inventory protection
        if not await self._check_inventory_protection(
            property_id, to_room_type, check_in_date
        ):
            return None
        
        # Get room rates
        from_rate = await self._get_room_rate(property_id, from_room_type, check_in_date)
        to_rate = await self._get_room_rate(property_id, to_room_type, check_in_date)
        base_upgrade_rate = to_rate - from_rate
        
        # Calculate multipliers
        demand_multiplier = await self._calculate_demand_multiplier(
            property_id, to_room_type, check_in_date
        )  # 0.8 to 1.5
        
        guest_value = await self._get_guest_value_score(guest_id)
        segment = self._get_guest_segment(guest_value)
        guest_value_factor = self._calculate_guest_value_factor(guest_value)  # 0.7 to 1.3
        
        days_until_checkin = (check_in_date - datetime.utcnow()).days
        timing_discount = self._calculate_timing_discount(days_until_checkin)  # 0.5 to 1.0
        
        inventory_adjustment = await self._calculate_inventory_adjustment(
            property_id, to_room_type, check_in_date
        )  # 0.8 to 1.2
        
        # Calculate final upgrade price
        upgrade_price = (
            base_upgrade_rate *
            Decimal(str(demand_multiplier)) *
            Decimal(str(guest_value_factor)) *
            Decimal(str(timing_discount)) *
            Decimal(str(inventory_adjustment))
        )
        
        # Apply segment discount
        discount_factor = self._get_segment_discount(segment, days_until_checkin)
        final_price = upgrade_price * discount_factor
        
        # Create offer
        offer = UpgradeOffer(
            offer_id=str(uuid4()),
            guest_id=guest_id,
            booking_id=await self._get_booking_id(guest_id, check_in_date),
            from_room=from_room_type,
            to_room=to_room_type,
            original_price=base_upgrade_rate,
            upgrade_price=upgrade_price,
            discount_factor=discount_factor,
            final_price=final_price,
            offer_sent=datetime.utcnow(),
            response_deadline=datetime.utcnow() + timedelta(hours=24),
            status='pending',
            channel=self._determine_channel(segment)
        )
        
        return offer
    
    async def _check_inventory_protection(
        self,
        property_id: str,
        room_type: str,
        check_in_date: datetime
    ) -> bool:
        """Prevent upgrades when predicted demand exceeds inventory."""
        
        forecasted_demand = await self.demand_forecaster.predict(
            property_id, room_type, check_in_date
        )
        available = await self._get_available_inventory(
            property_id, room_type, check_in_date
        )
        protection_threshold = self._calculate_protection_threshold(
            room_type, forecasted_demand
        )
        
        # Don't offer upgrade if:
        # 1. Available inventory <= protection threshold
        # 2. Forecasted demand > 80% of available
        if available <= protection_threshold:
            return False
        if forecasted_demand > (available * 0.8):
            return False
        
        return True
    
    def _calculate_timing_discount(self, days_until_checkin: int) -> float:
        """Higher discount closer to check-in."""
        if days_until_checkin >= 7:
            return 1.0
        elif days_until_checkin >= 5:
            return 0.9
        elif days_until_checkin >= 3:
            return 0.8
        elif days_until_checkin >= 1:
            return 0.6
        else:  # Day of arrival
            return 0.5
```

#### Guest Segmentation Matrix
| Segment | Value Score | Pricing Strategy | Discount Range | Offer Timing |
|---------|-------------|-----------------|----------------|--------------|
| VIP/Loyalty | 90-100 | Premium Experience | 0.6-0.8 | 7 days pre-arrival |
| High Spender | 70-89 | Value Enhancement | 0.7-0.9 | 5 days pre-arrival |
| Regular Guest | 50-69 | Standard Upgrade | 0.8-1.0 | 3 days pre-arrival |
| Price Sensitive | 30-49 | Last-minute Deals | 0.5-0.7 | Day of arrival |
| First-time | 0-29 | Experience Sampling | 0.6-0.8 | At check-in |

---

### SKILL-127: Early Check-in / Late Checkout

#### Purpose
Smart lock integration enabling automated flexible access with dynamic pricing and cleaning schedule coordination.

#### Technical Architecture
```python
from dataclasses import dataclass
from typing import Optional, Dict
from datetime import datetime, time
from decimal import Decimal

@dataclass
class AccessCode:
    code_id: str
    guest_id: str
    room_number: str
    code_value: str
    scheduled_start: datetime
    scheduled_end: datetime
    actual_start: Optional[datetime]
    actual_end: Optional[datetime]
    permissions: Dict[str, bool]  # main_door, room_door, amenity_access
    flexibility_fee: Decimal
    payment_status: str

@dataclass
class FlexibleAccessPricing:
    time_window: str
    base_fee: Decimal
    demand_multiplier: float
    cleaning_impact: Decimal
    final_price_range: tuple


class FlexibleAccessService:
    """
    Smart lock integration with dynamic access pricing.
    Door codes activate at check-in, expire 30 min after checkout.
    """
    
    PRICING_MATRIX = {
        'early_6_8am': FlexibleAccessPricing('6-8 AM', Decimal('25'), 1.0, Decimal('15'), (20, 45)),
        'early_8_10am': FlexibleAccessPricing('8-10 AM', Decimal('20'), 0.95, Decimal('10'), (18, 32)),
        'late_6_8pm': FlexibleAccessPricing('6-8 PM', Decimal('30'), 1.15, Decimal('20'), (30, 59)),
        'late_8_10pm': FlexibleAccessPricing('8-10 PM', Decimal('40'), 1.3, Decimal('25'), (44, 85)),
        'overnight': FlexibleAccessPricing('10 PM+', Decimal('60'), 1.5, Decimal('35'), (72, 143))
    }
    
    def __init__(self):
        self.smart_lock = SmartLockClient()  # Seam Universal API
        self.db = MongoDB()
        self.scheduler = CleaningScheduler()
        self.payment = StripeClient()
    
    async def request_early_checkin(
        self,
        booking_id: str,
        requested_time: datetime
    ) -> Dict:
        """Process early check-in request."""
        
        booking = await self._get_booking(booking_id)
        room = await self._get_room(booking['room_id'])
        
        # Check cleaning schedule conflict
        conflict = await self.scheduler.check_conflict(
            room['room_number'],
            booking['check_in_date'],
            requested_time
        )
        
        # Calculate price
        pricing_tier = self._get_pricing_tier(requested_time)
        base_fee = self.PRICING_MATRIX[pricing_tier].base_fee
        demand_multiplier = await self._get_demand_multiplier(
            booking['property_id'], booking['check_in_date']
        )
        cleaning_impact = self.PRICING_MATRIX[pricing_tier].cleaning_impact if conflict else Decimal('0')
        
        final_price = (base_fee * Decimal(str(demand_multiplier))) + cleaning_impact
        
        return {
            'available': not conflict or conflict.get('resolvable', False),
            'requested_time': requested_time.isoformat(),
            'price': float(final_price),
            'cleaning_conflict': conflict is not None,
            'conflict_resolution': conflict.get('resolution') if conflict else None
        }
    
    async def approve_flexible_access(
        self,
        booking_id: str,
        access_type: str,  # 'early_checkin' or 'late_checkout'
        requested_time: datetime,
        payment_method: str
    ) -> AccessCode:
        """Approve and process flexible access request."""
        
        booking = await self._get_booking(booking_id)
        
        # Process payment
        pricing = await self.request_early_checkin(booking_id, requested_time) \
            if access_type == 'early_checkin' \
            else await self.request_late_checkout(booking_id, requested_time)
        
        payment = await self.payment.charge(
            amount=Decimal(str(pricing['price'])),
            payment_method=payment_method,
            metadata={'type': 'flexible_access', 'booking_id': booking_id}
        )
        
        # Generate access code
        code_value = self._generate_secure_code()
        
        # Calculate access window
        if access_type == 'early_checkin':
            scheduled_start = requested_time
            scheduled_end = booking['check_out_date'] + timedelta(minutes=30)
        else:
            scheduled_start = booking['check_in_date']
            scheduled_end = requested_time + timedelta(minutes=30)
        
        # Create access code
        access_code = AccessCode(
            code_id=str(uuid4()),
            guest_id=booking['guest_id'],
            room_number=booking['room_number'],
            code_value=code_value,
            scheduled_start=scheduled_start,
            scheduled_end=scheduled_end,
            actual_start=None,
            actual_end=None,
            permissions={
                'main_door': True,
                'room_door': True,
                'amenity_access': True
            },
            flexibility_fee=Decimal(str(pricing['price'])),
            payment_status='paid'
        )
        
        # Program smart lock
        await self.smart_lock.create_access_code(
            device_id=await self._get_lock_device_id(booking['room_number']),
            code=code_value,
            starts_at=scheduled_start.isoformat(),
            ends_at=scheduled_end.isoformat()
        )
        
        # Update cleaning schedule if needed
        if pricing.get('cleaning_conflict'):
            await self.scheduler.reschedule(
                booking['room_number'],
                booking['check_in_date']
            )
        
        await self.db.access_codes.insert_one(asdict(access_code))
        
        return access_code
```

#### Pricing Matrix
| Time Window | Base Fee | Demand Range | Cleaning Impact | Price Range |
|-------------|----------|--------------|-----------------|-------------|
| Early (6-8 AM) | $25 | 0.8-1.2 | +$15 if conflict | $20-45 |
| Standard Early (8-10 AM) | $20 | 0.9-1.1 | +$10 if conflict | $18-32 |
| Late (6-8 PM) | $30 | 1.0-1.3 | +$20 if next booking | $30-59 |
| Extended Late (8-10 PM) | $40 | 1.1-1.5 | +$25 if next booking | $44-85 |
| Overnight (10 PM+) | $60 | 1.2-1.8 | +$35 if next booking | $72-143 |

---

### SKILL-055: Website SEO

#### Purpose
VacationRental structured data implementation enabling Google rich snippets with pricing, ratings, and amenity information for 15-25% direct booking increase.

#### Technical Architecture
```typescript
// Next.js Schema.org Implementation
interface VacationRentalSchema {
  '@context': 'https://schema.org';
  '@type': 'VacationRental';
  name: string;
  description: string;
  url: string;
  image: string[];
  address: PostalAddress;
  geo: GeoCoordinates;
  amenityFeature: LocationFeatureSpecification[];
  numberOfRooms: number;
  floorSize: QuantitativeValue;
  occupancy: QuantitativeValue;
  priceRange: string;
  aggregateRating?: AggregateRating;
  review?: Review[];
}

// Dynamic Schema Generator
class VacationRentalSchemaGenerator {
  async generateSchema(propertyId: string): Promise<VacationRentalSchema> {
    const property = await this.getPropertyData(propertyId);
    const reviews = await this.getReviews(propertyId);
    const pricing = await this.getCurrentPricing(propertyId);
    
    return {
      '@context': 'https://schema.org',
      '@type': 'VacationRental',
      name: property.name,
      description: property.description,
      url: `https://${property.domain}/${property.slug}`,
      image: property.images.map(img => img.url),
      address: {
        '@type': 'PostalAddress',
        streetAddress: property.address.street,
        addressLocality: property.address.city,
        addressRegion: property.address.state,
        postalCode: property.address.postal_code,
        addressCountry: property.address.country
      },
      geo: {
        '@type': 'GeoCoordinates',
        latitude: property.location.lat.toString(),
        longitude: property.location.lng.toString()
      },
      amenityFeature: property.amenities.map(amenity => ({
        '@type': 'LocationFeatureSpecification',
        name: amenity.name,
        value: amenity.available
      })),
      numberOfRooms: property.bedrooms,
      floorSize: {
        '@type': 'QuantitativeValue',
        value: property.square_feet,
        unitCode: 'SQF'
      },
      occupancy: {
        '@type': 'QuantitativeValue',
        maxValue: property.max_guests
      },
      priceRange: `$${pricing.min_price}-$${pricing.max_price}`,
      aggregateRating: reviews.length > 0 ? {
        '@type': 'AggregateRating',
        ratingValue: this.calculateAverageRating(reviews).toString(),
        reviewCount: reviews.length.toString()
      } : undefined,
      review: reviews.slice(0, 5).map(review => ({
        '@type': 'Review',
        author: {
          '@type': 'Person',
          name: review.author_name
        },
        reviewRating: {
          '@type': 'Rating',
          ratingValue: review.rating.toString()
        },
        reviewBody: review.text
      }))
    };
  }
}

// Next.js Page with Schema
export default function PropertyPage({ property, schema }) {
  return (
    <>
      <Head>
        <title>{property.name} | Book Direct</title>
        <meta name="description" content={property.description} />
        <script
          type="application/ld+json"
          dangerouslySetInnerHTML={{ __html: JSON.stringify(schema) }}
        />
      </Head>
      <PropertyContent property={property} />
    </>
  );
}

export async function getStaticProps({ params }) {
  const property = await getProperty(params.slug);
  const schema = await generateSchema(property.id);
  
  return {
    props: { property, schema },
    revalidate: 3600 // Regenerate every hour
  };
}
```

#### SEO Content Strategy
| Content Type | Update Frequency | SEO Impact | Implementation |
|--------------|------------------|------------|----------------|
| Property Availability | Real-time | High | Dynamic schema updates |
| Pricing Information | Daily | High | Structured data refresh |
| Guest Reviews | Weekly | Medium | Review schema integration |
| Local Attractions | Monthly | Medium | Content marketing blog |
| Neighborhood Guides | Quarterly | High | Long-form SEO content |
| Event Calendars | Weekly | Medium | Local event integration |

#### Core Web Vitals Targets
| Metric | Target | Measurement |
|--------|--------|-------------|
| LCP (Largest Contentful Paint) | <2.5s | Lighthouse |
| FID (First Input Delay) | <100ms | Chrome UX Report |
| CLS (Cumulative Layout Shift) | <0.1 | Lighthouse |

---

## 🗄️ DATABASE SCHEMA

### MongoDB Collections

```javascript
// Guest Profile Collection
{
  "_id": "ObjectId",
  "personalInfo": {
    "firstName": "string",
    "lastName": "string",
    "email": "string",
    "phone": "string"
  },
  "preferences": {
    "roomType": "string",
    "floorPreference": "number",
    "amenities": ["string"],
    "dietaryRestrictions": ["string"],
    "communicationPreferences": {
      "email": "boolean",
      "sms": "boolean",
      "push": "boolean"
    }
  },
  "loyaltyProgram": {
    "tier": "string",
    "points": "number",
    "memberSince": "date"
  },
  "gdprConsent": {
    "marketing": { "granted": "boolean", "grantedAt": "date" },
    "dataProcessing": { "granted": "boolean", "grantedAt": "date" }
  }
}

// Upgrade Offer Collection
{
  "_id": "ObjectId",
  "bookingId": "ObjectId",
  "guestId": "ObjectId",
  "fromRoom": "string",
  "toRoom": "string",
  "pricing": {
    "originalPrice": "Decimal128",
    "upgradePrice": "Decimal128",
    "discountFactor": "Decimal128",
    "finalPrice": "Decimal128"
  },
  "timing": {
    "offerSent": "date",
    "responseDeadline": "date",
    "guestResponse": "date"
  },
  "status": "string",
  "channel": "string"
}

// Experience Booking Collection
{
  "_id": "ObjectId",
  "bookingId": "ObjectId",
  "provider": {
    "id": "string",
    "name": "string"
  },
  "experience": {
    "externalId": "string",
    "title": "string",
    "category": "string"
  },
  "commission": {
    "rate": "Decimal128",
    "amount": "Decimal128",
    "netRevenue": "Decimal128"
  },
  "status": "string"
}

// Indexes
db.guests.createIndex({ "personalInfo.email": 1 }, { unique: true });
db.guests.createIndex({ "loyaltyProgram.tier": 1, "createdAt": -1 });
db.upgrade_offers.createIndex({ "bookingId": 1, "status": 1 });
db.experience_bookings.createIndex({ "provider.id": 1, "booking.date": -1 });
```

---

## 📊 PERFORMANCE REQUIREMENTS

| Skill | Response Time | Throughput | Availability |
|-------|--------------|------------|--------------|
| SKILL-087 (Front Desk) | <2s dashboard | 1000 concurrent | 99.9% |
| SKILL-124 (Concierge) | <3s recommendations | 500 req/min | 99.5% |
| SKILL-125 (Experience) | <5s booking | 100 bookings/min | 99.7% |
| SKILL-126 (Upgrades) | <1s pricing | 1000 calcs/min | 99.8% |
| SKILL-127 (Flex Access) | <10s code gen | 200 req/min | 99.9% |
| SKILL-055 (SEO) | <3s page load | CDN-scaled | 99.9% |

---

## 🔐 SECURITY CONSIDERATIONS

### Component Security Matrix
| Component | Authentication | Authorization | Encryption |
|-----------|---------------|---------------|------------|
| Front Desk | OAuth 2.0 + MFA | RBAC | TLS 1.3 + AES-256 |
| Concierge | API Key + JWT | Scope-based | TLS 1.3 |
| Experience | OAuth 2.0 + PCI | Payment roles | E2E encryption |
| Upgrades | JWT + rate limit | Revenue roles | TLS 1.3 |
| Flex Access | Device certs | Physical access | MQTT TLS |
| SEO | API auth | Content roles | TLS 1.3 + CDN |

### Compliance
- **PCI DSS**: Payment card protection
- **GDPR**: Guest data privacy (7-year retention)
- **SOC 2**: Security controls
- **CCPA**: California privacy rights

---

## 📁 FILE LOCATIONS

```
specs/hospitality/
└── SPEC-SKILL-055-127-HOSPITALITY-PREMIUM.md (this file)

knowledge/hospitality/
└── KD-PHASE2-G7-hospitality-premium.md (research source)

skills/hospitality/
├── SKILL-087-front-desk-command-center.md
├── SKILL-124-digital-concierge.md
├── SKILL-125-experience-booking.md
├── SKILL-126-room-upgrade-management.md
├── SKILL-127-early-checkin-late-checkout.md
└── SKILL-055-website-seo.md
```

---

## 🚀 IMPLEMENTATION ROADMAP

| Week | Milestone |
|------|-----------|
| 1-2 | SKILL-087 (Front Desk) + WebSocket infrastructure |
| 3-4 | SKILL-126 (Upgrades) + pricing algorithms |
| 5-6 | SKILL-124 (Concierge) + GPT-4 integration |
| 7-8 | SKILL-125 (Experience) + Viator/GetYourGuide APIs |
| 9-10 | SKILL-127 (Flex Access) + smart lock integration |
| 11-12 | SKILL-055 (SEO) + schema implementation |

---

**Status**: ✅ SPECIFIED - Ready for Engineering Implementation

