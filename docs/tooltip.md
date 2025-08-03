# Tooltip Components for ShadcnUI

Tooltip components provide contextual information and guidance through small overlay messages that appear on hover or focus, enhancing user understanding without cluttering the interface. The Shadcn UI tooltip system delivers accessible, customizable information overlays that support various content types and positioning options.

## Common Use Cases

- **Contextual help** providing additional information about interface elements and features
- **Icon explanations** clarifying the purpose of iconographic interface elements
- **Truncated content** showing full text for abbreviated or shortened content
- **Feature guidance** introducing new functionality and interface improvements
- **Status information** displaying detailed status or metadata for interface elements
- **Keyboard shortcuts** showing available keyboard combinations and quick actions

## Where Tooltip Components Get Used

Tooltip interfaces appear throughout interactive applications:
- **Navigation interfaces**: Menu explanations, icon clarifications, shortcut displays, feature descriptions
- **Form controls**: Field help, validation guidance, format examples, input assistance
- **Dashboard elements**: Metric explanations, chart details, widget information, status clarification
- **Toolbar interfaces**: Tool descriptions, action explanations, feature introductions, shortcut hints
- **Data displays**: Cell details, truncated content, metadata information, context explanations
- **Interactive elements**: Button purposes, link destinations, feature availability, state information

Tooltips enhance usability by providing just-in-time information without interface clutter.

## Implementation Examples

Let's explore different tooltip implementations with production-ready code you can use immediately using the most popular ShadcnUI component and block library - [SERP Blocks](https://serp.ly/serp-blocks)

<a href="https://serp.ly/serp-blocks" target="_blank">
<img width="966" height="728" alt="image" src="https://github.com/user-attachments/assets/73f6f02e-e3f7-491f-bfd4-446ad569bd84" />
</a>

## Example 1: Enhanced Tooltip System

```jsx
import {
  Tooltip,
  TooltipContent,
  TooltipProvider,
  TooltipTrigger,
} from "@/components/ui/tooltip"
import { Button } from "@/components/ui/button"
import { Badge } from "@/components/ui/badge"
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from "@/components/ui/card"
import { Avatar, AvatarFallback, AvatarImage } from "@/components/ui/avatar"
import {
  Save,
  Share2,
  Download,
  Settings,
  Help,
  Info,
  Calendar,
  User,
  Mail,
  Phone,
  MapPin,
  Star,
  Heart,
  Bookmark,
  MoreHorizontal,
  Keyboard,
  Zap
} from "lucide-react"

export function EnhancedTooltipSystem() {
  const toolbarActions = [
    {
      icon: Save,
      label: "Save",
      description: "Save your current work",
      shortcut: "Ctrl+S",
      disabled: false
    },
    {
      icon: Share2,
      label: "Share",
      description: "Share with team members",
      shortcut: "Ctrl+Shift+S",
      disabled: false
    },
    {
      icon: Download,
      label: "Download",
      description: "Download as PDF or image",
      shortcut: "Ctrl+D",
      disabled: false
    },
    {
      icon: Settings,
      label: "Settings",
      description: "Configure application preferences",
      shortcut: "Ctrl+,",
      disabled: false
    },
    {
      icon: Help,
      label: "Help",
      description: "Access help documentation",
      shortcut: "F1",
      disabled: false
    }
  ]

  const userData = {
    name: "Sarah Johnson",
    email: "sarah.johnson@company.com",
    phone: "+1 (555) 123-4567",
    location: "San Francisco, CA",
    role: "Senior Designer",
    avatar: "/api/placeholder/40/40",
    status: "online",
    joinDate: "March 2022"
  }

  return (
    <TooltipProvider>
      <div className="space-y-6 max-w-4xl mx-auto">
        {/* Toolbar with Tooltips */}
        <Card>
          <CardHeader>
            <CardTitle className="flex items-center gap-2">
              <Zap className="h-5 w-5" />
              Interactive Toolbar
            </CardTitle>
            <CardDescription>
              Hover over buttons to see contextual information and keyboard shortcuts
            </CardDescription>
          </CardHeader>
          <CardContent>
            <div className="flex items-center gap-2 p-3 bg-muted/50 rounded-lg">
              {toolbarActions.map((action) => {
                const Icon = action.icon
                return (
                  <Tooltip key={action.label}>
                    <TooltipTrigger asChild>
                      <Button
                        variant="ghost"
                        size="icon"
                        disabled={action.disabled}
                        className="h-9 w-9"
                      >
                        <Icon className="h-4 w-4" />
                      </Button>
                    </TooltipTrigger>
                    <TooltipContent side="bottom" className="max-w-xs">
                      <div className="space-y-1">
                        <div className="font-semibold">{action.label}</div>
                        <div className="text-sm text-muted-foreground">
                          {action.description}
                        </div>
                        <div className="flex items-center gap-2 pt-1">
                          <Keyboard className="h-3 w-3" />
                          <span className="text-xs font-mono bg-muted px-1 rounded">
                            {action.shortcut}
                          </span>
                        </div>
                      </div>
                    </TooltipContent>
                  </Tooltip>
                )
              })}
            </div>
          </CardContent>
        </Card>

        {/* User Profile with Rich Tooltips */}
        <Card>
          <CardHeader>
            <CardTitle>User Profile Information</CardTitle>
            <CardDescription>
              Profile elements with detailed tooltip information
            </CardDescription>
          </CardHeader>
          <CardContent>
            <div className="flex items-start gap-6">
              <Tooltip>
                <TooltipTrigger asChild>
                  <div className="relative">
                    <Avatar className="h-16 w-16 cursor-pointer">
                      <AvatarImage src={userData.avatar} />
                      <AvatarFallback>
                        {userData.name.split(' ').map(n => n[0]).join('')}
                      </AvatarFallback>
                    </Avatar>
                    <div className={`absolute -bottom-1 -right-1 h-4 w-4 rounded-full border-2 border-background ${
                      userData.status === 'online' ? 'bg-green-500' : 'bg-gray-400'
                    }`} />
                  </div>
                </TooltipTrigger>
                <TooltipContent side="right" className="max-w-sm">
                  <div className="space-y-3">
                    <div className="flex items-center gap-3">
                      <Avatar className="h-12 w-12">
                        <AvatarImage src={userData.avatar} />
                        <AvatarFallback>
                          {userData.name.split(' ').map(n => n[0]).join('')}
                        </AvatarFallback>
                      </Avatar>
                      <div>
                        <div className="font-semibold">{userData.name}</div>
                        <div className="text-sm text-muted-foreground">{userData.role}</div>
                        <div className="flex items-center gap-1 mt-1">
                          <div className={`h-2 w-2 rounded-full ${
                            userData.status === 'online' ? 'bg-green-500' : 'bg-gray-400'
                          }`} />
                          <span className="text-xs capitalize">{userData.status}</span>
                        </div>
                      </div>
                    </div>
                    
                    <div className="space-y-2 text-sm">
                      <div className="flex items-center gap-2">
                        <Mail className="h-3 w-3" />
                        <span>{userData.email}</span>
                      </div>
                      <div className="flex items-center gap-2">
                        <Phone className="h-3 w-3" />
                        <span>{userData.phone}</span>
                      </div>
                      <div className="flex items-center gap-2">
                        <MapPin className="h-3 w-3" />
                        <span>{userData.location}</span>
                      </div>
                      <div className="flex items-center gap-2">
                        <Calendar className="h-3 w-3" />
                        <span>Joined {userData.joinDate}</span>
                      </div>
                    </div>
                  </div>
                </TooltipContent>
              </Tooltip>

              <div className="flex-1 space-y-2">
                <h3 className="text-xl font-semibold">{userData.name}</h3>
                <p className="text-muted-foreground">{userData.role}</p>
                
                <div className="flex items-center gap-4 pt-2">
                  <Tooltip>
                    <TooltipTrigger asChild>
                      <Button variant="ghost" size="sm" className="text-muted-foreground">
                        <Mail className="h-4 w-4 mr-2" />
                        Contact
                      </Button>
                    </TooltipTrigger>
                    <TooltipContent>
                      <p>Send email to {userData.email}</p>
                    </TooltipContent>
                  </Tooltip>

                  <Tooltip>
                    <TooltipTrigger asChild>
                      <Button variant="ghost" size="sm" className="text-muted-foreground">
                        <User className="h-4 w-4 mr-2" />
                        Profile
                      </Button>
                    </TooltipTrigger>
                    <TooltipContent>
                      <p>View full profile and work history</p>
                    </TooltipContent>
                  </Tooltip>
                </div>
              </div>
            </div>
          </CardContent>
        </Card>

        {/* Action Buttons with Contextual Tooltips */}
        <Card>
          <CardHeader>
            <CardTitle>Quick Actions</CardTitle>
            <CardDescription>
              Action buttons with contextual help and status information
            </CardDescription>
          </CardHeader>
          <CardContent>
            <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
              <Tooltip>
                <TooltipTrigger asChild>
                  <Button variant="outline" className="h-16 flex flex-col gap-1">
                    <Star className="h-5 w-5" />
                    <span className="text-xs">Favorite</span>
                  </Button>
                </TooltipTrigger>
                <TooltipContent>
                  <div className="space-y-1">
                    <div className="font-semibold">Add to Favorites</div>
                    <div className="text-sm text-muted-foreground">
                      Save this item for quick access later
                    </div>
                  </div>
                </TooltipContent>
              </Tooltip>

              <Tooltip>
                <TooltipTrigger asChild>
                  <Button variant="outline" className="h-16 flex flex-col gap-1">
                    <Heart className="h-5 w-5" />
                    <span className="text-xs">Like</span>
                    <Badge variant="secondary" className="text-xs">24</Badge>
                  </Button>
                </TooltipTrigger>
                <TooltipContent>
                  <div className="space-y-1">
                    <div className="font-semibold">24 people liked this</div>
                    <div className="text-sm text-muted-foreground">
                      Click to add your reaction
                    </div>
                  </div>
                </TooltipContent>
              </Tooltip>

              <Tooltip>
                <TooltipTrigger asChild>
                  <Button variant="outline" className="h-16 flex flex-col gap-1">
                    <Bookmark className="h-5 w-5" />
                    <span className="text-xs">Save</span>
                  </Button>
                </TooltipTrigger>
                <TooltipContent>
                  <div className="space-y-1">
                    <div className="font-semibold">Bookmark</div>
                    <div className="text-sm text-muted-foreground">
                      Save to your reading list
                    </div>
                    <div className="flex items-center gap-1 pt-1">
                      <Keyboard className="h-3 w-3" />
                      <span className="text-xs font-mono bg-muted px-1 rounded">Ctrl+B</span>
                    </div>
                  </div>
                </TooltipContent>
              </Tooltip>

              <Tooltip>
                <TooltipTrigger asChild>
                  <Button variant="outline" className="h-16 flex flex-col gap-1">
                    <MoreHorizontal className="h-5 w-5" />
                    <span className="text-xs">More</span>
                  </Button>
                </TooltipTrigger>
                <TooltipContent>
                  <div className="space-y-1">
                    <div className="font-semibold">More Actions</div>
                    <div className="text-sm text-muted-foreground">
                      Access additional options and settings
                    </div>
                  </div>
                </TooltipContent>
              </Tooltip>
            </div>
          </CardContent>
        </Card>

        {/* Information Tooltips */}
        <Card>
          <CardHeader>
            <CardTitle className="flex items-center gap-2">
              Project Statistics
              <Tooltip>
                <TooltipTrigger asChild>
                  <Info className="h-4 w-4 text-muted-foreground cursor-help" />
                </TooltipTrigger>
                <TooltipContent>
                  <p>Statistics are updated in real-time and reflect current project state</p>
                </TooltipContent>
              </Tooltip>
            </CardTitle>
          </CardHeader>
          <CardContent>
            <div className="grid grid-cols-3 gap-4 text-center">
              <div>
                <Tooltip>
                  <TooltipTrigger asChild>
                    <div className="cursor-help">
                      <div className="text-2xl font-bold">156</div>
                      <div className="text-sm text-muted-foreground">Total Tasks</div>
                    </div>
                  </TooltipTrigger>
                  <TooltipContent>
                    <div className="space-y-1">
                      <div className="font-semibold">Task Breakdown</div>
                      <div className="text-sm space-y-1">
                        <div>• 89 Completed (57%)</div>
                        <div>• 45 In Progress (29%)</div>
                        <div>• 22 Pending (14%)</div>
                      </div>
                    </div>
                  </TooltipContent>
                </Tooltip>
              </div>

              <div>
                <Tooltip>
                  <TooltipTrigger asChild>
                    <div className="cursor-help">
                      <div className="text-2xl font-bold">8</div>
                      <div className="text-sm text-muted-foreground">Team Members</div>
                    </div>
                  </TooltipTrigger>
                  <TooltipContent>
                    <div className="space-y-1">
                      <div className="font-semibold">Active Contributors</div>
                      <div className="text-sm text-muted-foreground">
                        Team members who contributed this week
                      </div>
                    </div>
                  </TooltipContent>
                </Tooltip>
              </div>

              <div>
                <Tooltip>
                  <TooltipTrigger asChild>
                    <div className="cursor-help">
                      <div className="text-2xl font-bold">73%</div>
                      <div className="text-sm text-muted-foreground">Progress</div>
                    </div>
                  </TooltipTrigger>
                  <TooltipContent>
                    <div className="space-y-1">
                      <div className="font-semibold">Project Completion</div>
                      <div className="text-sm text-muted-foreground">
                        Based on completed milestones and task progress
                      </div>
                    </div>
                  </TooltipContent>
                </Tooltip>
              </div>
            </div>
          </CardContent>
        </Card>
      </div>
    </TooltipProvider>
  )
}
```

- **Use Case:** Interface guidance, contextual help, feature explanation
- **Key Features:** Rich content tooltips, keyboard shortcuts, status information
- **Customization:** Add custom positioning, implement delay controls, include multimedia content

## Installation & Setup

To implement tooltip components in your project:

```bash
npx shadcn-ui@latest add tooltip
```

Additional components for enhanced tooltips:
```bash
npx shadcn-ui@latest add button badge card avatar
```

Basic usage patterns:
```jsx
import {
  Tooltip,
  TooltipContent,
  TooltipProvider,
  TooltipTrigger,
} from "@/components/ui/tooltip"

// Basic tooltip
<TooltipProvider>
  <Tooltip>
    <TooltipTrigger asChild>
      <Button variant="outline">Hover me</Button>
    </TooltipTrigger>
    <TooltipContent>
      <p>This is a tooltip</p>
    </TooltipContent>
  </Tooltip>
</TooltipProvider>

// Positioned tooltip
<Tooltip>
  <TooltipTrigger asChild>
    <Button>Button</Button>
  </TooltipTrigger>
  <TooltipContent side="right" align="start">
    <p>Tooltip content</p>
  </TooltipContent>
</Tooltip>
```

## Best Practices

## Content Guidelines
- Keep tooltip content concise and relevant
- Provide actionable information when appropriate
- Use consistent tone and language across tooltips
- Include keyboard shortcuts when applicable
- Avoid duplicating visible interface text
- Test tooltip content with various languages

## Accessibility Requirements
- Ensure tooltips are keyboard accessible and discoverable
- Provide proper ARIA attributes for screen reader support
- Use appropriate timing for tooltip appearance and dismissal
- Test with assistive technologies for complete accessibility
- Ensure tooltip content is meaningful and helpful
- Provide alternative access methods for tooltip information

## Performance Considerations
- Implement efficient tooltip positioning calculations
- Use proper event handling to avoid performance issues
- Consider tooltip content loading for dynamic information
- Optimize tooltip rendering for large numbers of elements
- Monitor tooltip performance in complex interfaces
- Implement proper cleanup for tooltip event listeners

## Conclusion

Tooltip components provide essential contextual information that enhances user understanding without cluttering interfaces. Proper implementation with accessible design, thoughtful content, and appropriate positioning creates helpful, unobtrusive information overlays.

By designing tooltip systems that provide timely, relevant information through accessible interaction patterns, you can create interfaces that guide users effectively while maintaining clean, focused layouts.

---

**Meta Description:** Learn how to implement accessible, informative tooltip components that provide contextual help and guidance without cluttering interfaces using Shadcn UI.

**Key Takeaways:**
- Tooltip components provide contextual information without interface clutter
- Proper positioning and timing create helpful, non-intrusive information overlays
- Accessibility features ensure tooltips work for all users and interaction methods
- Rich content support enables detailed explanations and guidance
- Performance optimization ensures tooltips don't impact application responsiveness

**Related Topics:**
- shadcn popover
- shadcn hover-card
- shadcn button
- shadcn accessibility
- shadcn help

**Social Media Snippets:**
1. "Build helpful tooltip systems that guide users without getting in the way! 💬 #webdev #tooltip #uidesign"

2. "Master contextual help with accessible, informative tooltip components ✨ #frontend #accessibility #userexperience"

3. "Stop confusing interfaces! Create helpful, timely guidance with great tooltips 🚀 #webdevelopment #ux"