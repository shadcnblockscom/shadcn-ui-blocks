# Dialog Components for ShadcnUI

A dialog component (also known as a modal) is an overlay UI element that appears on top of the main content, requiring user interaction before returning to the application. Dialogs create a focused experience by dimming or blocking the background content, drawing complete attention to a specific task, message, or decision. They're built with accessibility in mind, managing focus states, keyboard navigation, and screen reader announcements to ensure all users can interact with them effectively.

Let's explore different card implementations with production-ready code you can use immediately using the most popular ShadcnUI component and block library - [SERP Blocks](https://serp.ly/serp-blocks)

<a href="https://serp.ly/serp-blocks" target="_blank">
<img width="966" height="728" alt="image" src="https://github.com/user-attachments/assets/73f6f02e-e3f7-491f-bfd4-446ad569bd84" />
</a>

### Common Use Cases

- **Confirmation dialogs** for destructive actions like deleting data or canceling changes
- **Form submissions** requiring focused input without page navigation
- **Content previews** displaying detailed information without leaving the current context
- **Authentication flows** for login, registration, or password reset
- **Settings panels** allowing users to modify preferences in a contained interface
- **Media galleries** showing images or videos in an immersive overlay

### Where Dialog Components Get Used

Dialogs appear across virtually every type of modern application:
- **E-commerce sites**: Quick product views, cart additions, checkout confirmations
- **SaaS applications**: Feature tours, upgrade prompts, data export options
- **Content platforms**: Article sharing, comment forms, subscription offers
- **Admin dashboards**: Bulk actions, detailed record views, configuration changes
- **Social media**: Post creation, media uploads, privacy settings
- **Enterprise software**: Approval workflows, document previews, multi-step processes

Dialogs can be triggered from buttons, links, keyboard shortcuts, or programmatically based on user behavior.

### Component Anatomy

A typical dialog component consists of:
- **Overlay/Backdrop**: Semi-transparent background that covers the main content
- **Dialog container**: The main modal window with defined boundaries
- **Dialog header**: Title and close button (optional but recommended)
- **Dialog content**: Main body containing forms, text, or other components
- **Dialog footer**: Action buttons like Save, Cancel, or Delete
- **Focus trap**: Invisible boundary keeping keyboard focus within dialog
- **Portal**: Renders dialog outside normal DOM hierarchy to avoid z-index issues

### Key JavaScript/Logic Concepts

Dialog components require sophisticated interaction handling:
- **State management**: Open/closed state, form data, loading states
- **Focus management**: Trapping focus, returning focus to trigger element on close
- **Keyboard handling**: Escape to close, Tab cycling, Enter to submit
- **Click outside detection**: Closing when clicking the backdrop
- **Animation coordination**: Entry/exit transitions, preventing layout shift
- **Scroll locking**: Preventing body scroll while dialog is open
- **Accessibility features**: ARIA attributes, live regions, role management

## Implementation Examples

Let's explore different dialog implementations with production-ready code you can use immediately.

### Example 1: Confirmation Dialog with Destructive Action

```jsx
import * as React from "react"
import {
  AlertDialog,
  AlertDialogAction,
  AlertDialogCancel,
  AlertDialogContent,
  AlertDialogDescription,
  AlertDialogFooter,
  AlertDialogHeader,
  AlertDialogTitle,
  AlertDialogTrigger,
} from "@/components/ui/alert-dialog"
import { Button } from "@/components/ui/button"
import { Trash2, AlertTriangle } from "lucide-react"

export function DeleteConfirmationDialog({ itemName, onDelete }) {
  const [isDeleting, setIsDeleting] = React.useState(false)

  const handleDelete = async () => {
    setIsDeleting(true)
    try {
      await onDelete()
    } finally {
      setIsDeleting(false)
    }
  }

  return (
    <AlertDialog>
      <AlertDialogTrigger asChild>
        <Button variant="destructive" size="sm">
          <Trash2 className="h-4 w-4 mr-2" />
          Delete
        </Button>
      </AlertDialogTrigger>
      <AlertDialogContent>
        <AlertDialogHeader>
          <div className="flex items-center gap-2">
            <div className="flex h-10 w-10 items-center justify-center rounded-full bg-red-100 dark:bg-red-900/20">
              <AlertTriangle className="h-5 w-5 text-red-600 dark:text-red-400" />
            </div>
            <AlertDialogTitle>Delete {itemName}?</AlertDialogTitle>
          </div>
          <AlertDialogDescription className="text-left">
            This action cannot be undone. This will permanently delete{" "}
            <span className="font-medium">{itemName}</span> and remove all associated data 
            from our servers.
          </AlertDialogDescription>
        </AlertDialogHeader>
        <AlertDialogFooter>
          <AlertDialogCancel disabled={isDeleting}>Cancel</AlertDialogCancel>
          <AlertDialogAction
            onClick={handleDelete}
            disabled={isDeleting}
            className="bg-red-600 hover:bg-red-700 focus:ring-red-600"
          >
            {isDeleting ? (
              <>
                <span className="loading loading-spinner loading-xs mr-2" />
                Deleting...
              </>
            ) : (
              "Delete"
            )}
          </AlertDialogAction>
        </AlertDialogFooter>
      </AlertDialogContent>
    </AlertDialog>
  )
}
```

- **Use Case:** Deleting records, canceling subscriptions, removing users, clearing data
- **Key Features:** Destructive styling, loading states, clear warning message, icon emphasis
- **Customization:** Adjust warning severity, add additional confirmation steps, customize messaging

### Example 2: Multi-Step Form Dialog

```jsx
import * as React from "react"
import {
  Dialog,
  DialogContent,
  DialogDescription,
  DialogFooter,
  DialogHeader,
  DialogTitle,
  DialogTrigger,
} from "@/components/ui/dialog"
import { Button } from "@/components/ui/button"
import { Input } from "@/components/ui/input"
import { Label } from "@/components/ui/label"
import { Textarea } from "@/components/ui/textarea"
import { RadioGroup, RadioGroupItem } from "@/components/ui/radio-group"
import { Progress } from "@/components/ui/progress"
import { ArrowLeft, ArrowRight, Check, Plus } from "lucide-react"

export function MultiStepFormDialog() {
  const [open, setOpen] = React.useState(false)
  const [currentStep, setCurrentStep] = React.useState(1)
  const [formData, setFormData] = React.useState({
    projectName: "",
    projectType: "",
    description: "",
    budget: "",
    timeline: "",
  })

  const totalSteps = 3

  const handleNext = () => {
    if (currentStep < totalSteps) {
      setCurrentStep(currentStep + 1)
    }
  }

  const handleBack = () => {
    if (currentStep > 1) {
      setCurrentStep(currentStep - 1)
    }
  }

  const handleSubmit = () => {
    console.log
