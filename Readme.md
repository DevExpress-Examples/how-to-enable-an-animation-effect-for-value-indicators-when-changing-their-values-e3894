<!-- default file list -->
*Files to look at*:

* [MainForm.cs](./CS/WindowsApplication3/MainForm.cs) (VB: [MainForm.vb](./VB/WindowsApplication3/MainForm.vb))
* [Program.cs](./CS/WindowsApplication3/Program.cs) (VB: [Program.vb](./VB/WindowsApplication3/Program.vb))
<!-- default file list end -->
# How to enable an animation effect for value indicators when changing their values


<p>To create the impression that a scale indicator changes its values smoothly, set the <a href="http://documentation.devexpress.com/#WindowsForms/DevExpressXtraGaugesWinGaugesCircularArcScaleComponent_EnableAnimationtopic"><u>ArcScaleComponent.EnableAnimation</u></a>/<a href="http://documentation.devexpress.com/#WindowsForms/DevExpressXtraGaugesWinGaugesLinearLinearScaleComponent_EnableAnimationtopic"><u>LinearScaleComponent.EnableAnimation</u></a> property to true. </p><p>To determine an animation function associated with how values are changed during animation, set the <a href="http://documentation.devexpress.com/#WindowsForms/DevExpressXtraGaugesWinGaugesCircularArcScaleComponent_EasingFunctiontopic"><u>ArcScaleComponent.EasingFunction</u></a>/<a href="http://documentation.devexpress.com/#WindowsForms/DevExpressXtraGaugesWinGaugesLinearLinearScaleComponent_EasingFunctiontopic"><u>LinearScaleComponent.EasingFunction</u></a> property to an <strong>IEasingFunction</strong><strong> </strong>object. </p><p>You can learn what animation functions exist by reviewing classes implementing the <strong>IEasingFunction</strong><strong> interface </strong>below:</p><p>     

```cs
public class BackEase : IEasingFunction {<newline/>		public double Ease(double normalizedTime) {<newline/>			double amplitude = 0.3;<newline/>			return (Math.Pow(normalizedTime, 3.0) - ((normalizedTime * amplitude) * Math.Sin(3.14 * normalizedTime)));<newline/>		}<newline/>	}<newline/>	public class ElasticEase : IEasingFunction {<newline/>		public double Ease(double normalizedTime) {<newline/>			double shift = (Math.Exp(6 * normalizedTime) - 1.0) / (Math.Exp(6) - 1.0);<newline/>			return (shift * Math.Sin(((6.28 * 3) + 1.57) * normalizedTime));<newline/>		}<newline/>	}<newline/>	public class BounceEase : IEasingFunction {<newline/>		public double Ease(double normalizedTime) {<newline/>			double bounce = 3;<newline/>			double degreeBounce = Math.Floor(Math.Log((-(normalizedTime * 26.5) * ( -2)) + 1.0, bounce));<newline/>			double correctionFactorNumerator = (1.0 - Math.Pow(bounce, degreeBounce)) / (-53);<newline/>			double correctionFactorDenominator = (1.0 - Math.Pow(bounce, degreeBounce + 1)) / (-53);<newline/>			double denominatorResult = -Math.Pow(bounce, degreeBounce) / (-53);<newline/>			return (((-Math.Pow(1.0 / bounce, 3 - degreeBounce) / (Math.Pow(denominatorResult,2))) * (normalizedTime - correctionFactorDenominator)) * (normalizedTime - correctionFactorNumerator));<newline/>		}<newline/>	}<newline/>	public class PowerEase : IEasingFunction {<newline/>		protected int degree;<newline/>		public PowerEase(int newDegree) {<newline/>			degree = newDegree;<newline/>		}<newline/>		public virtual double Ease(double normalizedTime) {<newline/>			double result = normalizedTime;<newline/>			for(int i = 1; i < degree; i++) {<newline/>				result *= normalizedTime;<newline/>			}<newline/>			return result;<newline/>		}<newline/>	}<newline/>	public class CubicEase : PowerEase {<newline/>		public CubicEase()<newline/>			: base(3) {<newline/>		}<newline/>	}<newline/>	public class QuadraticEase : PowerEase {<newline/>		public QuadraticEase()<newline/>			: base(2) {<newline/>		}<newline/>	}<newline/>	public class QuinticEase : PowerEase {<newline/>		public QuinticEase()<newline/>			: base(4) {<newline/>		}<newline/>	}<newline/>	public class SineEase : IEasingFunction {<newline/>		public double Ease(double normalizedTime) {<newline/>			return (1.0 - Math.Sin(1.57 * (1.0 - normalizedTime)));<newline/>		}<newline/>	}<newline/>	public class ExponentialEase : IEasingFunction {<newline/>		public double Ease(double normalizedTime) {<newline/>			return (Math.Exp(7 * normalizedTime) - 1.0) / (Math.Exp(7) - 1.0);<newline/>		}<newline/>	}<newline/>public class CircleEase : IEasingFunction {<newline/>		public double Ease(double normalizedTime) {<newline/>			return (1.0 - Math.Sqrt(1.0 - (normalizedTime * normalizedTime)));<newline/>		}<newline/>	}<newline/>
<newline/>
```

In addition, you can set how the animation is interpolated via the <a href="http://documentation.devexpress.com/#WindowsForms/DevExpressXtraGaugesWinGaugesCircularArcScaleComponent_EasingModetopic"><u>ArcScaleComponent.EasingMode</u></a>/<a href="http://documentation.devexpress.com/#WindowsForms/DevExpressXtraGaugesWinGaugesLinearLinearScaleComponent_EasingModetopic"><u>LinearScaleComponent.EasingMode</u></a> property to EaseIn, EaseInOut or EaseOut. </p><p>This example demonstrates how to enable animated changing of indicator values. </p><p> </p>

<br/>


