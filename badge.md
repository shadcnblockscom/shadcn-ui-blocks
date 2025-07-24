# Badge Components for ShadcnUI

Badges draw attention to short pieces of information—think of them as labels or tags for UI elements.  
Shadcn UI describes the badge component succinctly: it **“displays a badge or a component that looks like a badge”**【390905259168285†L120-L121】.  
Badges are perfect for highlighting statuses, categories or counts without overwhelming your design.

## Common Use Cases

- Indicating statuses such as “New,” “Beta” or “Sale.”  
- Labeling items with categories or tags.  
- Displaying notification counts on icons.  
- Calling attention to actionable text in lists or tables.

## Where Badge Components Get Used

- E‑commerce sites for product labels.  
- Dashboards to highlight new features or warnings.  
- Email clients and messaging apps for unread counts.  
- Documentation sites to mark deprecated APIs or experimental features.

## Component Anatomy

- **Badge** – the wrapper element that applies background, text color and border radius.  
- **Icon or text** – badges can contain plain text or icons to communicate meaning.  
- **Variants** – different styles such as default, destructive, outline or secondary depending on context.

## Key JavaScript/Logic Concepts

- Choosing the right variant based on semantic meaning (e.g., error vs. success).  
- Passing props to control size, color and icons.  
- Composing badges with other components like buttons or cards.  
- Using dynamic data (e.g., unread count) to render badge content.

## Implementation Example: Notification Badge

Here’s how to add a badge indicating unread messages on a mail icon.

```tsx
import { Badge } from "@/components/ui/badge";
import { Mail } from "lucide-react";

export function InboxButton({ unread }: { unread: number }) {
  return (
    <button className="relative inline-flex items-center gap-2 p-2 rounded-md hover:bg-accent">
      <Mail className="h-5 w-5" />
      <span>Inbox</span>
      {unread > 0 && (
        <Badge className="ml-2" variant="destructive">
          {unread}
        </Badge>
      )}
    </button>
  );
}
```

**Use Case:** Show unread message counts on navigation items.  
**Key Features:** Variants like `destructive` or `outline` for semantic emphasis; supports numbers or text; easy composition.  
**Customization & Theming:** Change the background using CSS variables, adjust padding for different sizes, or add icons for more context.

## Installation & Setup

1. Run the initialization command if you’re new to Shadcn UI:  
   ```sh
   pnpm dlx shadcn@latest init
   ```
2. Add the badge component using the CLI:  
   ```sh
   pnpm dlx shadcn@latest add badge
   ```  
   This installs the badge files and registers CSS variables【390905259168285†L172-L179】.

Import the `Badge` component from `@/components/ui/badge` and pass the `variant` prop to change its appearance.

## Best Practices

- **Keep badges short:** Use one or two words or a small number to avoid wrapping.  
- **Semantic colors:** Match colors to the meaning (e.g., red for errors, green for success).  
- **Responsive design:** Reduce badge size on smaller screens to maintain legibility.  
- **Accessibility:** Provide context via `aria-label` or tooltips if the badge alone isn’t descriptive.  
- **Testing:** Ensure dynamic counts update correctly and don’t overflow their container.

## Conclusion

Badges are small but mighty UI elements that call attention to important information.  With Shadcn UI you can quickly add stylish badges to your app using variants that fit your brand.  Whether labeling products or counting notifications, badges keep users informed at a glance.

## Meta Description

Learn how to implement badges in Shadcn UI.  This guide covers usage scenarios, installation and customization for labels, statuses and counts【390905259168285†L120-L121】.

## Key Takeaways

- Badges emphasize concise information such as statuses and counts【390905259168285†L120-L121】.  
- The Shadcn UI badge component supports variants and icons out of the box.  
- Use the CLI to install the component and import from `@/components/ui/badge`【390905259168285†L172-L179】.