# Button Components for ShadcnUI

Buttons are fundamental interactive elements that trigger actions.  
The Shadcn UI documentation defines the button component as one that **“displays a button or a component that looks like a button”**.  
With Shadcn UI, buttons come in multiple variants (primary, secondary, destructive, link) and sizes out of the box.

## Common Use Cases

- Submitting forms or triggering events.  
- Opening dialogs, modals or popovers.  
- Navigating to other pages when styled as links.  
- Performing destructive actions like delete or reset.

## Where Button Components Get Used

- Web applications of every type: dashboards, e‑commerce, marketing.  
- Mobile responsive interfaces requiring large tappable targets.  
- Toolbars and control panels.  
- Forms and settings pages.

## Component Anatomy

- **Button** – the main element that accepts variant and size props.  
- **Icon (optional)** – include icons before or after the label for clarity.  
- **Loading indicator** – a spinner or skeleton to indicate a pending action.  
- **Variants** – styles such as `default`, `destructive`, `outline`, `secondary` and `ghost`.

## Key JavaScript/Logic Concepts

- Handling `onClick` callbacks to run functions or navigate.  
- Disabling buttons during asynchronous operations.  
- Using `type="submit"` for form submission.  
- Composing buttons with `Link` components for navigation while preserving styles.

## Implementation Example: Primary Action Button

Here’s how to create a primary button that triggers a toast notification when clicked.

```tsx
import { Button } from "@/components/ui/button";
import { useToast } from "@/components/ui/use-toast";

export default function SaveButton() {
  const { toast } = useToast();
  function handleSave() {
    // perform save logic here
    toast({ title: "Saved", description: "Your changes have been saved." });
  }
  return (
    <Button onClick={handleSave} variant="default">
      Save Changes
    </Button>
  );
}
```

**Use Case:** Submit data and inform the user of success.  
**Key Features:** Variants for different semantic actions, built‑in focus styles, disabled state.  
**Customization & Theming:** Adjust size with the `size` prop, change colors via CSS variables, or create custom variants in your Tailwind config.

## Installation & Setup

1. Initialize your Shadcn project if you haven’t already:  
   ```sh
   pnpm dlx shadcn@latest init
   ```
2. Install the button component:  
   ```sh
   pnpm dlx shadcn@latest add button
   ```  
   This sets up the button files and registers CSS variables.

Import the `Button` component from `@/components/ui/button` and pass `variant` and `size` props as needed.

## Best Practices

- **Clarity:** Use descriptive labels that tell users what will happen.  
- **Disable during processing:** Prevent multiple clicks while asynchronous operations are running.  
- **Semantic variants:** Choose variants that match the action (e.g., destructive for delete).  
- **Accessible focus:** Ensure focus indicators are visible for keyboard users.  
- **Testing:** Confirm that click handlers fire correctly and disabled states behave as expected.

## Conclusion

Buttons are the workhorses of any interface.  Shadcn UI provides flexible, accessible button components with sensible defaults and multiple variants.  Incorporate them into your forms, toolbars and navigation to create clear, actionable interfaces.

## Meta Description

Explore the Shadcn UI button component.  Learn how to implement variants, handle click events and customise buttons for any action.

## Key Takeaways

- Buttons trigger actions and come in various semantic variants.  
- Install the button component via the Shadcn UI CLI.  
- Customise size, variant and content to fit your design.