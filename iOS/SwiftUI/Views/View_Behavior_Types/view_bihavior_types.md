In SwiftUI, views generally fall into two layout behaviors based on how they respond to size proposals from their parent: Content-Driven (Ideal Sized) and Layout-Flexible (Space-Absorbing).

1. Content-Driven Views
These views size themselves strictly around their content or natural intrinsic size. When a parent proposes a size, a content-driven view takes only what it needs (or clips/truncates if offered less than its minimum).
 Textual & Display Content: ⁠Text⁠, ⁠Image⁠ (by default, non-resizable), ⁠Label⁠, ⁠SF Symbol⁠ icons (⁠Image(systemName:)⁠).
 Controls & Inputs: ⁠Button⁠, ⁠Toggle⁠, ⁠TextField⁠, ⁠SecureField⁠, ⁠Slider⁠, ⁠Stepper⁠, ⁠DatePicker⁠, ⁠ColorPicker⁠, ⁠Picker⁠.
 Indicators & Decorative: ⁠ProgressView⁠ (spinner style), ⁠Divider⁠ (fixed thickness, though flexible in length).
 Shapes with explicit constraints: Any view wrapped in fixed ⁠.frame(width:height:)⁠.

2. Layout-Flexible Views
These views ignore intrinsic size and expand to fill all available space proposed by their parent container.
 Vector Shapes: ⁠Rectangle⁠, ⁠RoundedRectangle⁠, ⁠Circle⁠, ⁠Ellipse⁠, ⁠Capsule⁠, ⁠Path⁠.
 Layout Fillers & Backgrounds: ⁠Spacer⁠, ⁠Color⁠ (e.g., ⁠Color.blue⁠ acts as a view that fills all offered space), ⁠LinearGradient⁠, ⁠RadialGradient⁠, ⁠AngularGradient⁠, ⁠Material⁠ backgrounds (e.g., ⁠.ultraThinMaterial⁠).
 Container Views: ⁠ZStack⁠, ⁠GeometryReader⁠ (always expands to take up the full proposed space of its parent).

3. Adaptive & Container Views
Some views dynamically change their sizing behavior based on their children, configuration, or environment:
 Stacks (⁠VStack⁠, ⁠HStack⁠): They take the sum of their children's sizes plus spacing. If any child inside them is layout-flexible (like a ⁠Spacer⁠ or ⁠Rectangle⁠), the stack becomes layout-flexible along that axis.
 Resizable Images: Calling ⁠.resizable()⁠ on an ⁠Image⁠ turns it from a content-driven view into a layout-flexible view.
 Scroll Containers (⁠ScrollView⁠, ⁠List⁠, ⁠Form⁠, ⁠Grid⁠): Expand to take up available space offered by the parent screen, but create an scrollable region for their content.
 ![](./VIew_Layout_Behavior.jpe)