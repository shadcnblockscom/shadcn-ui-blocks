# Spinner Components for ShadcnUI

Spinner components provide visual feedback for loading states and processing operations, offering users clear indication that the system is working on their request. The Shadcn UI spinner system delivers accessible, customizable loading indicators that maintain user engagement during wait times while following modern design principles.

## Common Use Cases

- **Button loading states** showing progress during form submissions or API calls
- **Page transitions** indicating navigation or route changes in progress
- **Data fetching** displaying loading states while content loads from servers
- **File uploads** showing progress during media or document uploads
- **Background processing** indicating ongoing tasks like report generation
- **Real-time updates** showing when live data is being refreshed or synchronized

## Where Spinner Components Get Used

Spinner loading appears throughout interactive applications:
- **Form submissions**: Contact forms, registration, checkout processes, data entry
- **Content loading**: Articles, images, videos, user-generated content, search results
- **Dashboard updates**: Analytics refresh, metric calculations, report generation
- **E-commerce interactions**: Cart updates, payment processing, inventory checks, order placement
- **File operations**: Document uploads, image processing, backup operations, sync processes
- **Real-time features**: Chat loading, notification updates, live data feeds, collaborative editing

Spinners provide essential feedback that maintains user confidence during system operations.

## Implementation Examples

Let's explore different spinner implementations with production-ready code you can use immediately using the most popular ShadcnUI component and block library - [SERP Blocks](https://serp.ly/serp-blocks)

<a href="https://serp.ly/serp-blocks" target="_blank">
<img width="966" height="728" alt="image" src="https://github.com/user-attachments/assets/73f6f02e-e3f7-491f-bfd4-446ad569bd84" />
</a>

## Example 1: Button Loading States

```jsx
import { Button } from "@/components/ui/button"
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card"
import { Loader2, Send, Download, Save, Upload, ShoppingCart } from "lucide-react"
import { useState } from "react"

export function ButtonLoadingStates() {
  const [loadingStates, setLoadingStates] = useState({})

  const handleClick = async (buttonId) => {
    setLoadingStates(prev => ({ ...prev, [buttonId]: true }))
    
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 2000))
    
    setLoadingStates(prev => ({ ...prev, [buttonId]: false }))
  }

  const buttons = [
    {
      id: "submit",
      label: "Submit Form",
      icon: Send,
      variant: "default"
    },
    {
      id: "save",
      label: "Save Changes",
      icon: Save,
      variant: "secondary"
    },
    {
      id: "download",
      label: "Download Report",
      icon: Download,
      variant: "outline"
    },
    {
      id: "upload",
      label: "Upload File",
      icon: Upload,
      variant: "destructive"
    },
    {
      id: "purchase",
      label: "Add to Cart",
      icon: ShoppingCart,
      variant: "default"
    }
  ]

  return (
    <Card>
      <CardHeader>
        <CardTitle>Button Loading States</CardTitle>
      </CardHeader>
      <CardContent className="space-y-4">
        <div className="grid gap-4 md:grid-cols-2">
          {buttons.map((button) => {
            const Icon = button.icon
            const isLoading = loadingStates[button.id]
            
            return (
              <Button
                key={button.id}
                variant={button.variant}
                onClick={() => handleClick(button.id)}
                disabled={isLoading}
                className="w-full"
              >
                {isLoading ? (
                  <>
                    <Loader2 className="mr-2 h-4 w-4 animate-spin" />
                    Loading...
                  </>
                ) : (
                  <>
                    <Icon className="mr-2 h-4 w-4" />
                    {button.label}
                  </>
                )}
              </Button>
            )
          })}
        </div>
        
        {/* Icon Only Buttons */}
        <div className="flex gap-2 pt-4 border-t">
          <Button
            size="icon"
            variant="outline"
            onClick={() => handleClick("icon1")}
            disabled={loadingStates.icon1}
          >
            {loadingStates.icon1 ? (
              <Loader2 className="h-4 w-4 animate-spin" />
            ) : (
              <Send className="h-4 w-4" />
            )}
          </Button>
          
          <Button
            size="icon"
            onClick={() => handleClick("icon2")}
            disabled={loadingStates.icon2}
          >
            {loadingStates.icon2 ? (
              <Loader2 className="h-4 w-4 animate-spin" />
            ) : (
              <Save className="h-4 w-4" />
            )}
          </Button>
        </div>
      </CardContent>
    </Card>
  )
}
```

- **Use Case:** Form submissions, data operations, user actions
- **Key Features:** Multiple button variants, disabled states, text and icon combinations
- **Customization:** Add progress percentages, implement timeout handling, include success states

## Example 2: Content Loading Spinners

```jsx
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card"
import { Loader2, RefreshCw, Download, Zap } from "lucide-react"
import { useState, useEffect } from "react"

export function ContentLoadingSpinners() {
  const [loadingStates, setLoadingStates] = useState({
    content: true,
    data: false,
    refresh: false
  })

  useEffect(() => {
    // Simulate initial content loading
    const timer = setTimeout(() => {
      setLoadingStates(prev => ({ ...prev, content: false }))
    }, 3000)
    
    return () => clearTimeout(timer)
  }, [])

  const startDataLoad = () => {
    setLoadingStates(prev => ({ ...prev, data: true }))
    setTimeout(() => {
      setLoadingStates(prev => ({ ...prev, data: false }))
    }, 2000)
  }

  const startRefresh = () => {
    setLoadingStates(prev => ({ ...prev, refresh: true }))
    setTimeout(() => {
      setLoadingStates(prev => ({ ...prev, refresh: false }))
    }, 1500)
  }

  return (
    <div className="space-y-6">
      {/* Page Loading */}
      <Card>
        <CardHeader>
          <CardTitle>Page Content Loading</CardTitle>
        </CardHeader>
        <CardContent className="min-h-[200px]">
          {loadingStates.content ? (
            <div className="flex items-center justify-center h-full">
              <div className="text-center space-y-4">
                <Loader2 className="h-8 w-8 animate-spin mx-auto text-primary" />
                <p className="text-muted-foreground">Loading content...</p>
              </div>
            </div>
          ) : (
            <div className="space-y-4">
              <h3 className="text-lg font-semibold">Content Loaded Successfully</h3>
              <p className="text-muted-foreground">
                This content was loaded asynchronously with a loading spinner to improve user experience.
              </p>
              <div className="grid gap-4 md:grid-cols-2">
                <div className="p-4 border rounded-lg">
                  <h4 className="font-medium mb-2">Feature 1</h4>
                  <p className="text-sm text-muted-foreground">Description of feature 1</p>
                </div>
                <div className="p-4 border rounded-lg">
                  <h4 className="font-medium mb-2">Feature 2</h4>
                  <p className="text-sm text-muted-foreground">Description of feature 2</p>
                </div>
              </div>
            </div>
          )}
        </CardContent>
      </Card>

      {/* Inline Loading States */}
      <div className="grid gap-4 md:grid-cols-2">
        <Card>
          <CardHeader className="flex flex-row items-center justify-between space-y-0">
            <CardTitle className="text-lg">Data Analysis</CardTitle>
            <button
              onClick={startDataLoad}
              disabled={loadingStates.data}
              className="p-2 rounded-md hover:bg-accent"
            >
              {loadingStates.data ? (
                <Loader2 className="h-4 w-4 animate-spin" />
              ) : (
                <Zap className="h-4 w-4" />
              )}
            </button>
          </CardHeader>
          <CardContent>
            {loadingStates.data ? (
              <div className="flex items-center gap-2 text-muted-foreground">
                <Loader2 className="h-4 w-4 animate-spin" />
                <span className="text-sm">Analyzing data...</span>
              </div>
            ) : (
              <div className="space-y-2">
                <div className="text-2xl font-bold">1,234</div>
                <div className="text-sm text-muted-foreground">Total Records</div>
              </div>
            )}
          </CardContent>
        </Card>

        <Card>
          <CardHeader className="flex flex-row items-center justify-between space-y-0">
            <CardTitle className="text-lg">Live Data</CardTitle>
            <button
              onClick={startRefresh}
              disabled={loadingStates.refresh}
              className="p-2 rounded-md hover:bg-accent"
            >
              {loadingStates.refresh ? (
                <Loader2 className="h-4 w-4 animate-spin" />
              ) : (
                <RefreshCw className="h-4 w-4" />
              )}
            </button>
          </CardHeader>
          <CardContent>
            {loadingStates.refresh ? (
              <div className="flex items-center gap-2 text-muted-foreground">
                <Loader2 className="h-4 w-4 animate-spin" />
                <span className="text-sm">Refreshing...</span>
              </div>
            ) : (
              <div className="space-y-2">
                <div className="text-2xl font-bold text-green-600">98.5%</div>
                <div className="text-sm text-muted-foreground">System Uptime</div>
              </div>
            )}
          </CardContent>
        </Card>
      </div>

      {/* Different Spinner Variants */}
      <Card>
        <CardHeader>
          <CardTitle>Spinner Variants</CardTitle>
        </CardHeader>
        <CardContent>
          <div className="flex items-center gap-8">
            <div className="text-center space-y-2">
              <Loader2 className="h-6 w-6 animate-spin mx-auto" />
              <p className="text-xs text-muted-foreground">Default</p>
            </div>
            
            <div className="text-center space-y-2">
              <div className="h-6 w-6 mx-auto border-2 border-primary border-t-transparent rounded-full animate-spin" />
              <p className="text-xs text-muted-foreground">Custom</p>
            </div>
            
            <div className="text-center space-y-2">
              <div className="flex space-x-1">
                <div className="h-2 w-2 bg-primary rounded-full animate-bounce [animation-delay:-0.3s]"></div>
                <div className="h-2 w-2 bg-primary rounded-full animate-bounce [animation-delay:-0.15s]"></div>
                <div className="h-2 w-2 bg-primary rounded-full animate-bounce"></div>
              </div>
              <p className="text-xs text-muted-foreground">Dots</p>
            </div>
            
            <div className="text-center space-y-2">
              <div className="h-6 w-6 mx-auto">
                <div className="h-full w-full border-4 border-gray-200 border-t-primary rounded-full animate-spin"></div>
              </div>
              <p className="text-xs text-muted-foreground">Ring</p>
            </div>
          </div>
        </CardContent>
      </Card>
    </div>
  )
}
```

- **Use Case:** Content loading, data refresh, async operations
- **Key Features:** Multiple spinner styles, inline loading states, refresh controls
- **Customization:** Add progress bars, implement skeleton loading, include error states

## Installation & Setup

Spinners typically use Lucide React icons with Tailwind CSS animations:

```bash
npm install lucide-react
```

Basic spinner implementations:
```jsx
import { Loader2 } from "lucide-react"

// Basic spinning icon
<Loader2 className="h-4 w-4 animate-spin" />

// Spinner with text
<div className="flex items-center gap-2">
  <Loader2 className="h-4 w-4 animate-spin" />
  <span>Loading...</span>
</div>

// Custom CSS spinner
<div className="h-6 w-6 border-2 border-primary border-t-transparent rounded-full animate-spin" />
```

Custom animations in Tailwind CSS:
```css
/* tailwind.config.js */
module.exports = {
  theme: {
    extend: {
      animation: {
        'spin-slow': 'spin 2s linear infinite',
        'pulse-fast': 'pulse 1s ease-in-out infinite',
        'bounce-fast': 'bounce 0.5s infinite',
      }
    }
  }
}
```

## Best Practices

## User Experience Guidelines
- Show spinners immediately when operations begin
- Use appropriate spinner sizes for different contexts
- Provide meaningful loading messages when possible
- Consider spinner duration and user patience
- Implement timeout handling for long operations
- Test spinner visibility across different themes and backgrounds

## Accessibility Requirements
- Include proper ARIA labels for loading states
- Provide screen reader announcements for loading progress
- Ensure spinner animations respect reduced motion preferences
- Use semantic loading indicators alongside visual spinners
- Test spinner interfaces with assistive technologies
- Implement proper focus management during loading states

## Performance Considerations
- Use CSS animations instead of JavaScript when possible
- Optimize spinner SVGs and icons for performance
- Consider spinner impact on battery life on mobile devices
- Implement efficient loading state management
- Avoid excessive re-renders during loading states
- Monitor spinner animation performance across devices

## Conclusion

Spinner components are essential for maintaining user engagement and confidence during loading states and processing operations. Proper implementation of loading indicators significantly improves perceived performance and user satisfaction.

By choosing appropriate spinner styles, implementing accessible loading states, and following performance best practices, you can create loading experiences that keep users informed and engaged throughout system operations.

---

**Meta Description:** Learn how to implement effective spinner loading components that improve user experience during processing and loading states with accessible design patterns.

**Key Takeaways:**
- Spinner components provide essential feedback during loading and processing operations
- Multiple spinner variants serve different use cases and design contexts
- Accessibility considerations ensure loading states work for all users
- Performance optimization prevents spinners from impacting application responsiveness
- Proper timing and messaging enhance user patience during wait times

**Related Topics:**
- shadcn loading
- shadcn button
- shadcn skeleton
- shadcn progress
- shadcn accessibility

**Social Media Snippets:**
1. "Keep users engaged with smooth, accessible loading spinners! ⚡ #webdev #loading #ux"

2. "Master loading states with spinners that enhance perceived performance ✨ #frontend #spinner #uidesign"

3. "Stop leaving users guessing! Create clear, professional loading experiences 🚀 #webdevelopment #userexperience"