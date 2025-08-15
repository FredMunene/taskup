# taskup - Base Minikit Accountability App
## MVP
## Project Overview
A token-rewarded accountability app built on Base Minikit that helps users complete tasks through buddy verification and social incentives. Users can optionally stake money to double their token rewards, creating stronger commitment mechanisms.

## Core Features

### 1. Task Creation & Management
- **Simple Task Input**: Clean interface for pasting/typing tasks
- **AI Task Analysis**: OpenAI integration to analyze task context and suggest deadlines
- **Task Categories**: Basic categorization (work, personal, health, etc.)
- **Timeline Management**: Set and track task deadlines
- **Task Status Tracking**: Pending → Active → Completed/Failed

### 2. Buddy System
- **Invite System**: Users can invite accountability partners via Coinbase Wallet addresses
- **Buddy Verification**: Partners confirm task completion through the app
- **Mutual Accountability**: Both users can verify each other's tasks
- **Buddy Matching**: Simple system to pair users who don't have partners
- **Trust Scoring**: Basic reputation system for reliable verification partners

### 3. Staking System (Optional)
- **Optional Stakes**: Users can choose to stake ETH/USDC on task completion
- **2x Token Multiplier**: Staked tasks earn double app tokens when completed
- **Stake Return**: Stakes are always returned regardless of completion status
- **Stake Amounts**: Flexible staking from $5 to $100+ 
- **Visual Stakes**: Clear UI showing staked vs non-staked tasks

### 4. Token Economy
- **Base ERC-20 Token**: Custom token minted on Base blockchain
- **Completion Rewards**: 
  - Non-staked tasks: 10-50 tokens (based on complexity/timeline)
  - Staked tasks: 20-100 base tokens (2x multiplier)
- **Streak Bonuses** (Staked Tasks Only):
  - 3 staked tasks in a row = 2.5x tokens
  - 5 staked tasks in a row = 3x tokens
  - 10 staked tasks in a row = 4x tokens
- **Weekly Challenges**: Complete 5 staked tasks this week = bonus 200 tokens
- **Verification Rewards**: 5-10 tokens for accurate buddy verification
- **Enhanced Gifting System**:
  - **Staked Gift Matching**: When gifting tokens, stakers get 50% bonus tokens to give
  - **Receiver Bonuses**: Gifts from stakers are worth 1.5x to recipients
- **Peer-to-Peer Gifting**: Users can tip tokens to encourage others
- **Token Balance Display**: Clear wallet integration showing token holdings

### 5. Social Features
- **Leaderboards**: Weekly/monthly token earnings rankings
- **Token Gifting**: Send tokens with encouragement messages
- **Achievement Sharing**: Broadcast completions to social feeds
- **Community Challenges**: Group goals and shared rewards (future feature)
- **Public Recognition**: Celebrate high performers and generous gifters

### 6. Base Minikit Integration
- **Native Wallet Connection**: Seamless Coinbase Wallet integration
- **Low-Cost Transactions**: Leverage Base's low gas fees
- **Mobile-First Design**: Optimized for mobile Coinbase Wallet
- **Push Notifications**: Task reminders and verification requests
- **Cross-App Integration**: Potential integration with other Base miniapps

## Technical Requirements

### Frontend
- **Framework**: React/Next.js miniapp
- **UI Library**: Base Minikit components
- **Wallet Integration**: Coinbase Wallet SDK
- **Mobile Optimization**: Responsive design for mobile-first usage

### Backend
- **API**: Next.js API routes
- **AI Integration**: OpenAI API for task analysis
- **Database**: Supabase for user data, tasks, and relationships
- **Blockchain RPC**: Base network integration

### Smart Contracts (Base)
```solidity
// Core functions needed:
- mintTaskToken(address user, uint256 baseAmount, uint256 streakMultiplier, bool staked)
- giftTokens(address from, address to, uint256 baseAmount, bool fromStaker)
- stakeForTask(bytes32 taskId, uint256 amount)
- returnStake(bytes32 taskId)
- verifyTaskCompletion(address user, bytes32 taskId, address verifier)
- updateStreakCounter(address user, bool successful)
- claimWeeklyChallenge(address user)
- getLeaderboard() returns (address[] memory, uint256[] memory)
- getStreakStatus(address user) returns (uint256 currentStreak, uint256 multiplier)
```

### Database Schema
```sql
-- Users
users: wallet_address, username, total_tokens, reputation_score, staked_streak, created_at

-- Tasks  
tasks: id, user_address, content, deadline, status, stake_amount, token_reward, is_staked, streak_position, created_at

-- Buddy Relationships
buddies: user_address, buddy_address, status, created_at

-- Verifications
verifications: task_id, verifier_address, verified_at, tokens_earned

-- Token Gifts
gifts: from_address, to_address, base_amount, bonus_amount, message, created_at

-- Weekly Challenges
weekly_challenges: user_address, week_start, staked_tasks_completed, challenge_completed, bonus_claimed
```

## User Flow

### 1. Onboarding
1. Connect Coinbase Wallet via Minikit
2. Set username and basic preferences  
3. Invite buddy or get matched with someone
4. Create first test task (no stake required)

### 2. Task Creation Flow
1. User inputs task text
2. AI analyzes and suggests deadline
3. User chooses to stake or not stake
4. If staking: select amount → approve transaction
5. Task created and buddy notified

### 3. Task Verification Flow
1. User marks task as complete
2. Buddy receives verification request
3. Buddy confirms completion (or disputes)
4. Smart contract mints appropriate tokens
5. If staked: stake returned + double tokens

### 4. Social Interaction Flow
1. Users can browse leaderboard
2. Gift tokens to encourage others
3. Share achievements publicly
4. Build reputation through consistent verification

## Success Metrics

### Engagement
- **Task Completion Rate**: Target 65%+ overall completion
- **Buddy Verification Rate**: 90%+ of completed tasks get verified
- **Token Gifting**: 20%+ of users gift tokens to others monthly
- **Return Usage**: 60%+ of users create multiple tasks

### Economic
- **Staking Adoption**: 30%+ of tasks are staked
- **Token Circulation**: Healthy peer-to-peer token flow
- **Wallet Connections**: Seamless onboarding via Minikit

### Social
- **Invite Rate**: Users invite average 1.5 friends
- **Community Growth**: Organic user acquisition through social features
- **Trust Network**: High buddy relationship satisfaction

## What We're NOT Building (V1)

### Deferred Features
- External calendar integration
- Complex reward marketplace  
- Advanced AI coaching
- Recurring/habit tasks
- Team challenges
- Premium subscriptions
- Cross-chain token bridging
- Advanced analytics dashboard

### Future Considerations
- Integration with other productivity apps
- Corporate/team versions
- Advanced staking strategies (pools, insurance)
- NFT achievements and badges
- DAO governance for platform decisions

## Revenue Model (Post-MVP)

### Potential Revenue Streams
1. **Transaction Fees**: Small percentage on token gifts and stakes
2. **Premium Features**: Advanced AI analysis, custom rewards
3. **Marketplace Commission**: Take cut from token-to-reward exchanges
4. **Corporate Licenses**: Team accountability solutions
5. **Sponsored Challenges**: Brands sponsor community challenges

## Development Priorities

### Phase 1 (MVP - 4-6 weeks)
1. Basic miniapp UI and wallet integration
2. Simple task creation and AI analysis
3. Buddy system and verification flow
4. Token smart contract deployment
5. Optional staking with 2x multiplier

### Phase 2 (Post-MVP - 2-4 weeks)
1. Leaderboards and social features
2. Token gifting system
3. Push notifications
4. Basic analytics and user dashboard

### Phase 3 (Growth - 4-8 weeks)
1. Advanced matching algorithms
2. Community challenges
3. External integrations
4. Monetization features

## Risk Considerations

### Technical Risks
- Smart contract security audits needed
- Base network stability and gas costs
- Minikit SDK limitations or changes
- AI API costs and reliability

### Product Risks  
- User adoption of staking mechanism
- Buddy system gaming/abuse
- Token value and utility perception
- Competition from established productivity apps

### Mitigation Strategies
- Start with small stakes and test with limited users
- Implement robust verification and reporting systems
- Focus on genuine utility over speculation
- Build strong community and network effects
