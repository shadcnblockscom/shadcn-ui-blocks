# Themes Components for ShadcnUI

Themes provide comprehensive visual styling systems that define color palettes, typography, spacing, and component appearance across applications. The Shadcn UI theming system enables consistent, customizable design languages that support brand identity, accessibility requirements, and user preferences like dark mode.

## Common Use Cases

- **Brand identity implementation** applying company colors, fonts, and visual styling
- **Dark mode support** providing alternative color schemes for low-light environments
- **Accessibility compliance** ensuring sufficient contrast and readable text across themes
- **User customization** allowing personal preference settings for visual appearance
- **Multi-tenant styling** supporting different visual themes for various clients or organizations
- **Seasonal variations** implementing temporary visual changes for holidays or campaigns

## Where Theme Systems Get Used

Theming appears across all types of modern applications:
- **Corporate applications**: Brand consistency, accessibility compliance, user preference support
- **SaaS platforms**: White-labeling, client customization, accessibility options, user experience personalization
- **E-commerce sites**: Brand reinforcement, seasonal styling, promotional themes, accessibility features
- **Content platforms**: Reading mode optimization, user preference accommodation, brand differentiation
- **Educational systems**: Institution branding, accessibility support, user customization options
- **Creative tools**: Theme variety, user preference support, accessibility compliance, brand expression

Theme systems ensure visual consistency while enabling customization and accessibility.

## Implementation Examples

Let's explore different theme implementations with production-ready code you can use immediately using the most popular ShadcnUI component and block library - [SERP Blocks](https://serp.ly/serp-blocks)

<a href="https://serp.ly/serp-blocks" target="_blank">
<img width="966" height="728" alt="image" src="https://github.com/user-attachments/assets/73f6f02e-e3f7-491f-bfd4-446ad569bd84" />
</a>

## Example 1: Theme Customization Panel

```jsx
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from "@/components/ui/card"
import { Button } from "@/components/ui/button"
import { Badge } from "@/components/ui/badge"
import { Label } from "@/components/ui/label"
import { Slider } from "@/components/ui/slider"
import { Switch } from "@/components/ui/switch"
import {
  Select,
  SelectContent,
  SelectItem,
  SelectTrigger,
  SelectValue,
} from "@/components/ui/select"
import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs"
import { 
  Palette, 
  Sun, 
  Moon, 
  Monitor, 
  Type, 
  Layout,
  Contrast,
  Eye,
  Zap,
  Settings
} from "lucide-react"
import { useState, useEffect } from "react"

const colorThemes = {
  blue: {
    name: "Ocean Blue",
    primary: "hsl(221, 83%, 53%)",
    secondary: "hsl(210, 40%, 96%)",
    accent: "hsl(210, 40%, 96%)",
    preview: "#3b82f6"
  },
  green: {
    name: "Forest Green", 
    primary: "hsl(142, 76%, 36%)",
    secondary: "hsl(138, 40%, 96%)",
    accent: "hsl(138, 40%, 96%)",
    preview: "#22c55e"
  },
  purple: {
    name: "Royal Purple",
    primary: "hsl(262, 83%, 58%)",
    secondary: "hsl(270, 40%, 96%)",
    accent: "hsl(270, 40%, 96%)",
    preview: "#8b5cf6"
  },
  orange: {
    name: "Sunset Orange",
    primary: "hsl(25, 95%, 53%)",
    secondary: "hsl(24, 40%, 96%)",
    accent: "hsl(24, 40%, 96%)",
    preview: "#f97316"
  }
}

const fontOptions = [
  { value: "inter", label: "Inter", preview: "font-sans" },
  { value: "roboto", label: "Roboto", preview: "font-sans" },
  { value: "poppins", label: "Poppins", preview: "font-sans" },
  { value: "system", label: "System Default", preview: "font-sans" }
]

export function ThemeCustomizationPanel() {
  const [currentTheme, setCurrentTheme] = useState("blue")
  const [mode, setMode] = useState("system")
  const [fontSize, setFontSize] = useState([16])
  const [borderRadius, setBorderRadius] = useState([0.5])
  const [animations, setAnimations] = useState(true)
  const [highContrast, setHighContrast] = useState(false)
  const [selectedFont, setSelectedFont] = useState("inter")

  useEffect(() => {
    const root = document.documentElement
    const theme = colorThemes[currentTheme]
    
    // Apply color theme
    root.style.setProperty('--primary', theme.primary)
    root.style.setProperty('--secondary', theme.secondary)
    root.style.setProperty('--accent', theme.accent)
    
    // Apply other settings
    root.style.setProperty('--base-font-size', `${fontSize[0]}px`)
    root.style.setProperty('--radius', `${borderRadius[0]}rem`)
    
    // Apply mode
    if (mode === "dark") {
      root.classList.add("dark")
    } else if (mode === "light") {
      root.classList.remove("dark")
    } else {
      // System preference
      const prefersDark = window.matchMedia("(prefers-color-scheme: dark)").matches
      root.classList.toggle("dark", prefersDark)
    }
    
    // Apply accessibility settings
    root.classList.toggle("high-contrast", highContrast)
    root.classList.toggle("reduce-motion", !animations)
  }, [currentTheme, mode, fontSize, borderRadius, animations, highContrast])

  return (
    <div className="space-y-6 max-w-4xl mx-auto">
      <Card>
        <CardHeader>
          <CardTitle className="flex items-center gap-2">
            <Palette className="h-5 w-5" />
            Theme Customization
          </CardTitle>
          <CardDescription>
            Customize the appearance and feel of your application
          </CardDescription>
        </CardHeader>
        <CardContent>
          <Tabs defaultValue="colors" className="space-y-4">
            <TabsList className="grid w-full grid-cols-4">
              <TabsTrigger value="colors">Colors</TabsTrigger>
              <TabsTrigger value="typography">Typography</TabsTrigger>
              <TabsTrigger value="layout">Layout</TabsTrigger>
              <TabsTrigger value="accessibility">Accessibility</TabsTrigger>
            </TabsList>

            <TabsContent value="colors" className="space-y-6">
              {/* Color Theme Selection */}
              <div className="space-y-3">
                <Label className="text-base font-semibold">Color Theme</Label>
                <div className="grid grid-cols-2 md:grid-cols-4 gap-3">
                  {Object.entries(colorThemes).map(([key, theme]) => (
                    <Button
                      key={key}
                      variant={currentTheme === key ? "default" : "outline"}
                      className="h-auto p-3 flex flex-col items-center gap-2"
                      onClick={() => setCurrentTheme(key)}
                    >
                      <div 
                        className="w-8 h-8 rounded-full border-2 border-white shadow-sm"
                        style={{ backgroundColor: theme.preview }}
                      />
                      <span className="text-sm">{theme.name}</span>
                    </Button>
                  ))}
                </div>
              </div>

              {/* Mode Selection */}
              <div className="space-y-3">
                <Label className="text-base font-semibold">Appearance Mode</Label>
                <div className="flex gap-2">
                  <Button
                    variant={mode === "light" ? "default" : "outline"}
                    onClick={() => setMode("light")}
                    className="flex items-center gap-2"
                  >
                    <Sun className="h-4 w-4" />
                    Light
                  </Button>
                  <Button
                    variant={mode === "dark" ? "default" : "outline"}
                    onClick={() => setMode("dark")}
                    className="flex items-center gap-2"
                  >
                    <Moon className="h-4 w-4" />
                    Dark
                  </Button>
                  <Button
                    variant={mode === "system" ? "default" : "outline"}
                    onClick={() => setMode("system")}
                    className="flex items-center gap-2"
                  >
                    <Monitor className="h-4 w-4" />
                    System
                  </Button>
                </div>
              </div>
            </TabsContent>

            <TabsContent value="typography" className="space-y-6">
              {/* Font Selection */}
              <div className="space-y-3">
                <Label className="text-base font-semibold">Font Family</Label>
                <Select value={selectedFont} onValueChange={setSelectedFont}>
                  <SelectTrigger>
                    <SelectValue />
                  </SelectTrigger>
                  <SelectContent>
                    {fontOptions.map((font) => (
                      <SelectItem key={font.value} value={font.value}>
                        <span className={font.preview}>{font.label}</span>
                      </SelectItem>
                    ))}
                  </SelectContent>
                </Select>
              </div>

              {/* Font Size */}
              <div className="space-y-3">
                <Label className="text-base font-semibold">
                  Font Size: {fontSize[0]}px
                </Label>
                <Slider
                  value={fontSize}
                  onValueChange={setFontSize}
                  max={24}
                  min={12}
                  step={1}
                  className="w-full"
                />
                <div className="text-sm text-muted-foreground">
                  Adjust the base font size for better readability
                </div>
              </div>
            </TabsContent>

            <TabsContent value="layout" className="space-y-6">
              {/* Border Radius */}
              <div className="space-y-3">
                <Label className="text-base font-semibold">
                  Border Radius: {borderRadius[0]}rem
                </Label>
                <Slider
                  value={borderRadius}
                  onValueChange={setBorderRadius}
                  max={1}
                  min={0}
                  step={0.1}
                  className="w-full"
                />
                <div className="text-sm text-muted-foreground">
                  Control the roundness of corners and borders
                </div>
              </div>

              {/* Animation Settings */}
              <div className="flex items-center justify-between">
                <div className="space-y-1">
                  <Label className="text-base font-semibold flex items-center gap-2">
                    <Zap className="h-4 w-4" />
                    Animations
                  </Label>
                  <div className="text-sm text-muted-foreground">
                    Enable smooth transitions and animations
                  </div>
                </div>
                <Switch
                  checked={animations}
                  onCheckedChange={setAnimations}
                />
              </div>
            </TabsContent>

            <TabsContent value="accessibility" className="space-y-6">
              {/* High Contrast */}
              <div className="flex items-center justify-between">
                <div className="space-y-1">
                  <Label className="text-base font-semibold flex items-center gap-2">
                    <Contrast className="h-4 w-4" />
                    High Contrast
                  </Label>
                  <div className="text-sm text-muted-foreground">
                    Increase contrast for better visibility
                  </div>
                </div>
                <Switch
                  checked={highContrast}
                  onCheckedChange={setHighContrast}
                />
              </div>

              {/* Accessibility Info */}
              <div className="p-4 bg-muted/50 rounded-lg space-y-2">
                <h4 className="font-semibold flex items-center gap-2">
                  <Eye className="h-4 w-4" />
                  Accessibility Features
                </h4>
                <ul className="text-sm space-y-1 text-muted-foreground">
                  <li>• Color contrast meets WCAG AA standards</li>
                  <li>• Font sizes scale for better readability</li>
                  <li>• Motion can be reduced for sensitivity</li>
                  <li>• High contrast mode available</li>
                  <li>• Keyboard navigation fully supported</li>
                </ul>
              </div>
            </TabsContent>
          </Tabs>
        </CardContent>
      </Card>

      {/* Theme Preview */}
      <Card>
        <CardHeader>
          <CardTitle>Preview</CardTitle>
          <CardDescription>See how your theme looks in practice</CardDescription>
        </CardHeader>
        <CardContent className="space-y-4">
          <div className="grid gap-4 md:grid-cols-3">
            <Card>
              <CardHeader>
                <CardTitle className="text-lg">Sample Card</CardTitle>
              </CardHeader>
              <CardContent>
                <p className="text-muted-foreground mb-4">
                  This is how cards will appear with your selected theme.
                </p>
                <div className="flex gap-2">
                  <Button size="sm">Primary</Button>
                  <Button variant="secondary" size="sm">Secondary</Button>
                </div>
              </CardContent>
            </Card>
            
            <Card>
              <CardHeader>
                <CardTitle className="text-lg">Typography</CardTitle>
              </CardHeader>
              <CardContent className="space-y-2">
                <h3 className="text-lg font-semibold">Heading Example</h3>
                <p className="text-sm text-muted-foreground">
                  Body text with your selected font and size settings.
                </p>
                <Badge>Sample Badge</Badge>
              </CardContent>
            </Card>
            
            <Card>
              <CardHeader>
                <CardTitle className="text-lg">Interactive Elements</CardTitle>
              </CardHeader>
              <CardContent className="space-y-2">
                <Button variant="outline" className="w-full">
                  <Settings className="mr-2 h-4 w-4" />
                  Settings Button
                </Button>
                <div className="flex items-center gap-2">
                  <Switch />
                  <Label>Toggle Switch</Label>
                </div>
              </CardContent>
            </Card>
          </div>
        </CardContent>
      </Card>
    </div>
  )
}
```

- **Use Case:** User customization, brand implementation, accessibility support
- **Key Features:** Live preview, accessibility options, comprehensive customization
- **Customization:** Add preset themes, implement theme sharing, include advanced color tools

## Installation & Setup

To implement theme systems in your project:

```bash
npx shadcn-ui@latest init
```

This sets up the basic theme system. For theme customization components:
```bash
npx shadcn-ui@latest add card button slider switch select tabs
```

CSS Variables Configuration:
```css
/* globals.css */
:root {
  --background: 0 0% 100%;
  --foreground: 222.2 84% 4.9%;
  --primary: 221.2 83.2% 53.3%;
  --primary-foreground: 210 40% 98%;
  --secondary: 210 40% 96%;
  --secondary-foreground: 222.2 84% 4.9%;
  --muted: 210 40% 96%;
  --muted-foreground: 215.4 16.3% 46.9%;
  --accent: 210 40% 96%;
  --accent-foreground: 222.2 84% 4.9%;
  --destructive: 0 84.2% 60.2%;
  --destructive-foreground: 210 40% 98%;
  --border: 214.3 31.8% 91.4%;
  --input: 214.3 31.8% 91.4%;
  --ring: 221.2 83.2% 53.3%;
  --radius: 0.5rem;
}

.dark {
  --background: 222.2 84% 4.9%;
  --foreground: 210 40% 98%;
  /* ... dark mode overrides */
}

.high-contrast {
  --background: 0 0% 100%;
  --foreground: 0 0% 0%;
  /* ... high contrast overrides */
}
```

## Best Practices

## Design System Integration
- Maintain consistent color relationships across theme variants
- Ensure accessibility compliance in all theme options
- Test themes with real content and various component combinations
- Document theme customization guidelines and limitations
- Provide fallbacks for unsupported CSS features
- Consider performance impact of dynamic theme switching

## User Experience Guidelines
- Provide intuitive theme selection interfaces
- Show live previews of theme changes
- Remember user preferences across sessions
- Respect system preferences as default settings
- Provide clear reset options for theme customization
- Consider onboarding for theme customization features

## Accessibility Compliance
- Ensure all theme variants meet WCAG contrast requirements
- Test themes with color blindness simulation tools
- Provide high contrast alternatives
- Support reduced motion preferences
- Test themes with screen readers and assistive technologies
- Document accessibility features and compliance levels

## Conclusion

Theme systems provide essential customization capabilities that enhance user experience, support accessibility requirements, and enable brand expression. Proper implementation of theming creates applications that adapt to user preferences while maintaining design consistency and accessibility standards.

By designing flexible theme systems with comprehensive customization options and accessibility considerations, you can create applications that serve diverse user needs while providing excellent visual experiences across all contexts and preferences.

---

**Meta Description:** Learn how to implement comprehensive theme systems with customization options, accessibility features, and brand support using Shadcn UI.

**Key Takeaways:**
- Theme systems enable consistent visual styling with customization flexibility
- Accessibility considerations ensure themes work for all users and preferences
- Live preview capabilities improve user experience during theme customization
- CSS custom properties enable efficient theme switching and customization
- Proper documentation and guidelines support theme system adoption and maintenance

**Related Topics:**
- shadcn mode
- shadcn colors
- shadcn accessibility
- shadcn customization
- shadcn design-system

**Social Media Snippets:**
1. "Build beautiful, accessible theme systems that adapt to every user's needs! 🎨 #webdev #themes #accessibility"

2. "Master visual customization with flexible, compliant theme implementations ✨ #frontend #uidesign #theming"

3. "Stop one-size-fits-all design! Create themes that work for everyone 🚀 #webdevelopment #accessibility"