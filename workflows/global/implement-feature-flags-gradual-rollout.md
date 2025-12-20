---
description: Safely release features with toggles for gradual rollouts
---

1. **Simple Approach: Environment Variables**:
   - Use env vars for basic flags.
   ```ts
   // lib/features.ts
   export const features = {
     newDashboard: process.env.NEXT_PUBLIC_FEATURE_NEW_DASHBOARD === 'true',
     aiChat: process.env.NEXT_PUBLIC_FEATURE_AI_CHAT === 'true',
   };
   ```

2. **Use in Components**:
   - Conditionally render features.
   ```tsx
   import { features } from '@/lib/features';
   
   export default function Dashboard() {
     if (features.newDashboard) {
       return <NewDashboard />;
     }
     return <OldDashboard />;
   }
   ```

3. **Advanced: Vercel Edge Config**:
   - Dynamic flags without redeployment.
   // turbo
   - Run `npm install @vercel/edge-config`
   ```ts
   import { get } from '@vercel/edge-config';
   
   export async function getFeatureFlags() {
     const flags = await get('features');
     return flags || {};
   }
   ```

4. **Production-Ready: LaunchDarkly/PostHog**:
   - Install SDK.
   // turbo
   - Run `npm install launchdarkly-react-client-sdk`
   ```tsx
   import { useLDClient, useFlags } from 'launchdarkly-react-client-sdk';
   
   function MyComponent() {
     const { newFeature } = useFlags();
     
     if (newFeature) {
       return <NewFeature />;
     }
     return <OldFeature />;
   }
   ```

5. **Gradual Rollout Pattern**:
   - Enable for percentage of users.
   ```ts
   function isFeatureEnabled(userId: string, rolloutPercent: number) {
     const hash = userId.split('').reduce((a, b) => a + b.charCodeAt(0), 0);
     return (hash % 100) < rolloutPercent;
   }
   
   const showNewUI = isFeatureEnabled(user.id, 25); // 25% rollout
   ```

6. **Pro Tips**:
   - Always have a kill switch for new features.
   - Log feature flag usage for analytics.
   - Clean up old flags after full rollout.
   - Use flags for A/B testing experiments.