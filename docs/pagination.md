# Pagination Components for ShadcnUI

Pagination components enable users to navigate through large datasets efficiently, providing clear navigation controls and status information for multi-page content. The Shadcn UI pagination system delivers accessible, customizable pagination patterns that maintain performance while offering intuitive navigation experiences across different content types and data volumes.

## Common Use Cases

- **Data table navigation** moving through large datasets with page-by-page browsing
- **Content listing pagination** navigating blog posts, articles, or product catalogs
- **Search result navigation** browsing through search findings with result counts
- **Gallery and media navigation** moving through image collections or video libraries
- **API result pagination** handling server-side pagination for database queries
- **Documentation navigation** browsing through help articles or knowledge bases

## Where Pagination Components Get Used

Pagination interfaces appear wherever content exceeds single-page display:
- **E-commerce platforms**: Product listings, category browsing, search results, order history
- **Content management systems**: Article lists, media galleries, user management, comment moderation
- **Data dashboards**: Transaction logs, user analytics, report listings, audit trails
- **Social platforms**: Feed browsing, follower lists, message histories, notification archives
- **Educational platforms**: Course catalogs, lesson listings, assignment galleries, grade books
- **Documentation sites**: Article collections, API references, tutorial series, FAQ sections

Pagination provides essential navigation for content-heavy applications and data-driven interfaces.

## Component Anatomy

A comprehensive pagination system includes:

- **Page numbers** – Clickable numeric navigation for direct page access
- **Navigation arrows** – Previous/next controls for sequential browsing
- **Current page indicator** – Clear visual indication of active page position
- **Page range display** – Truncated page lists for large pagination sets
- **Jump controls** – First/last page navigation for efficient browsing
- **Results summary** – Total count and current range information
- **Page size selector** – Options for adjusting items per page
- **Loading states** – Visual feedback during page transitions

These elements work together to create efficient, intuitive navigation experiences.

## Implementation Examples

Let's explore different pagination implementations with production-ready code you can use immediately using the most popular ShadcnUI component and block library - [SERP Blocks](https://serp.ly/serp-blocks)

<a href="https://serp.ly/serp-blocks" target="_blank">
<img width="966" height="728" alt="image" src="https://github.com/user-attachments/assets/73f6f02e-e3f7-491f-bfd4-446ad569bd84" />
</a>

## Example 1: Complete Pagination Component

```jsx
import {
  Pagination,
  PaginationContent,
  PaginationEllipsis,
  PaginationItem,
  PaginationLink,
  PaginationNext,
  PaginationPrevious,
} from "@/components/ui/pagination"
import {
  Select,
  SelectContent,
  SelectItem,
  SelectTrigger,
  SelectValue,
} from "@/components/ui/select"
import { Button } from "@/components/ui/button"
import { Card, CardContent } from "@/components/ui/card"
import { ChevronFirst, ChevronLast } from "lucide-react"

export function CompletePagination({
  currentPage = 1,
  totalPages = 10,
  totalItems = 250,
  itemsPerPage = 25,
  onPageChange,
  onItemsPerPageChange,
  showFirstLast = true,
  showPageSize = true,
  showSummary = true
}) {
  const startItem = (currentPage - 1) * itemsPerPage + 1
  const endItem = Math.min(currentPage * itemsPerPage, totalItems)

  const getVisiblePages = () => {
    const delta = 2
    const range = []
    const rangeWithDots = []

    for (
      let i = Math.max(2, currentPage - delta);
      i <= Math.min(totalPages - 1, currentPage + delta);
      i++
    ) {
      range.push(i)
    }

    if (currentPage - delta > 2) {
      rangeWithDots.push(1, '...')
    } else {
      rangeWithDots.push(1)
    }

    rangeWithDots.push(...range)

    if (currentPage + delta < totalPages - 1) {
      rangeWithDots.push('...', totalPages)
    } else if (totalPages > 1) {
      rangeWithDots.push(totalPages)
    }

    return rangeWithDots
  }

  return (
    <div className="space-y-4">
      {/* Summary */}
      {showSummary && (
        <div className="flex items-center justify-between text-sm text-muted-foreground">
          <span>
            Showing {startItem}-{endItem} of {totalItems} results
          </span>
          {showPageSize && (
            <div className="flex items-center gap-2">
              <span>Items per page:</span>
              <Select
                value={itemsPerPage.toString()}
                onValueChange={(value) => onItemsPerPageChange?.(parseInt(value))}
              >
                <SelectTrigger className="w-20">
                  <SelectValue />
                </SelectTrigger>
                <SelectContent>
                  <SelectItem value="10">10</SelectItem>
                  <SelectItem value="25">25</SelectItem>
                  <SelectItem value="50">50</SelectItem>
                  <SelectItem value="100">100</SelectItem>
                </SelectContent>
              </Select>
            </div>
          )}
        </div>
      )}

      {/* Pagination Controls */}
      <div className="flex items-center justify-center">
        <div className="flex items-center gap-2">
          {/* First Page */}
          {showFirstLast && (
            <Button
              variant="outline"
              size="icon"
              onClick={() => onPageChange?.(1)}
              disabled={currentPage === 1}
            >
              <ChevronFirst className="h-4 w-4" />
            </Button>
          )}

          {/* Pagination Component */}
          <Pagination>
            <PaginationContent>
              <PaginationItem>
                <PaginationPrevious
                  onClick={() => onPageChange?.(Math.max(1, currentPage - 1))}
                  isActive={currentPage > 1}
                />
              </PaginationItem>

              {getVisiblePages().map((page, index) => (
                <PaginationItem key={index}>
                  {page === '...' ? (
                    <PaginationEllipsis />
                  ) : (
                    <PaginationLink
                      onClick={() => onPageChange?.(page)}
                      isActive={currentPage === page}
                    >
                      {page}
                    </PaginationLink>
                  )}
                </PaginationItem>
              ))}

              <PaginationItem>
                <PaginationNext
                  onClick={() => onPageChange?.(Math.min(totalPages, currentPage + 1))}
                  isActive={currentPage < totalPages}
                />
              </PaginationItem>
            </PaginationContent>
          </Pagination>

          {/* Last Page */}
          {showFirstLast && (
            <Button
              variant="outline"
              size="icon"
              onClick={() => onPageChange?.(totalPages)}
              disabled={currentPage === totalPages}
            >
              <ChevronLast className="h-4 w-4" />
            </Button>
          )}
        </div>
      </div>
    </div>
  )
}
```

- **Use Case:** Data tables, content listings, search results
- **Key Features:** Complete navigation, page size selection, result summary
- **Customization:** Add keyboard navigation, implement URL synchronization, include loading states

## Example 2: Simple Navigation Pagination

```jsx
import { Button } from "@/components/ui/button"
import { Badge } from "@/components/ui/badge"
import { ChevronLeft, ChevronRight } from "lucide-react"

export function SimplePagination({
  currentPage = 1,
  totalPages = 5,
  onPageChange,
  showPageInfo = true
}) {
  const hasNext = currentPage < totalPages
  const hasPrevious = currentPage > 1

  return (
    <div className="flex items-center justify-between">
      <Button
        variant="outline"
        onClick={() => onPageChange?.(currentPage - 1)}
        disabled={!hasPrevious}
        className="flex items-center gap-2"
      >
        <ChevronLeft className="h-4 w-4" />
        Previous
      </Button>

      {showPageInfo && (
        <div className="flex items-center gap-2">
          <span className="text-sm text-muted-foreground">Page</span>
          <Badge variant="outline">{currentPage}</Badge>
          <span className="text-sm text-muted-foreground">of</span>
          <Badge variant="outline">{totalPages}</Badge>
        </div>
      )}

      <Button
        variant="outline"
        onClick={() => onPageChange?.(currentPage + 1)}
        disabled={!hasNext}
        className="flex items-center gap-2"
      >
        Next
        <ChevronRight className="h-4 w-4" />
      </Button>
    </div>
  )
}
```

- **Use Case:** Simple content navigation, blog posts, image galleries
- **Key Features:** Minimal interface, clear navigation, responsive design
- **Customization:** Add progress indicators, implement gesture support, include auto-advance

## Installation & Setup

To implement pagination components in your project:

```bash
npx shadcn-ui@latest add pagination
```

Additional components for enhanced pagination:
```bash
npx shadcn-ui@latest add button select badge
```

Basic usage patterns:
```jsx
import {
  Pagination,
  PaginationContent,
  PaginationItem,
  PaginationLink,
  PaginationNext,
  PaginationPrevious,
} from "@/components/ui/pagination"

// Basic pagination
<Pagination>
  <PaginationContent>
    <PaginationItem>
      <PaginationPrevious href="#" />
    </PaginationItem>
    <PaginationItem>
      <PaginationLink href="#">1</PaginationLink>
    </PaginationItem>
    <PaginationItem>
      <PaginationLink href="#" isActive>2</PaginationLink>
    </PaginationItem>
    <PaginationItem>
      <PaginationLink href="#">3</PaginationLink>
    </PaginationItem>
    <PaginationItem>
      <PaginationNext href="#" />
    </PaginationItem>
  </PaginationContent>
</Pagination>
```

## Best Practices

## User Experience Guidelines
- Provide clear indication of current page position
- Show total page count when space allows
- Include result summaries for context
- Ensure touch targets meet minimum size requirements
- Provide keyboard navigation support
- Test pagination with various data volumes

## Performance Considerations
- Implement efficient data fetching strategies
- Use proper caching for paginated results
- Consider virtual scrolling for very large datasets
- Optimize pagination for slow network connections
- Implement progressive loading where appropriate
- Monitor pagination performance metrics

## Accessibility Requirements
- Ensure pagination controls are keyboard accessible
- Provide proper ARIA labels and roles
- Include screen reader announcements for page changes
- Use semantic HTML for pagination structure
- Test with assistive technologies
- Provide alternative navigation methods when needed

## Conclusion

Pagination components are essential for managing large datasets and content collections efficiently. Shadcn UI's pagination system provides the flexibility and accessibility needed to create professional navigation experiences that scale with content volume while maintaining excellent usability.

By implementing proper pagination patterns, performance optimizations, and accessibility features, you can create navigation interfaces that help users browse content efficiently while maintaining excellent user experience standards.

---

**Meta Description:** Learn how to implement accessible, efficient pagination components for data navigation with Shadcn UI and responsive design patterns.

**Key Takeaways:**
- Pagination components enable efficient navigation through large datasets
- Proper page range handling prevents interface clutter with many pages
- Result summaries and page size controls enhance user experience
- Accessibility compliance ensures pagination works for all users
- Performance optimization is crucial for handling large datasets

**Related Topics:**
- shadcn button
- shadcn select
- shadcn table
- shadcn navigation
- shadcn loading

**Social Media Snippets:**
1. "Build efficient pagination that scales with your data! Navigate like a pro 📄 #webdev #pagination #uidesign"

2. "Master data navigation with accessible, performant pagination components ✨ #frontend #datatable #navigation"

3. "Stop overwhelming users with endless scrolling! Create smart pagination experiences 🚀 #webdevelopment #ux"