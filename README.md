```glsl
#version 410 core

// inputs
in vec2 vScreenCoord;

// uniforms
uniform vec4 uLinePoints;
uniform float uDistance;
uniform vec4 uColorInner;
uniform vec4 uColorOuter;

// outputs
layout (location = 0) out vec4 fragColor;

void main()
{
	// get distances
	vec2 p0 = vScreenCoord.xy;
	vec2 p1 = uLinePoints.xy;
	vec2 p2 = uLinePoints.zw;
	float dist = 
		abs((p2.x - p1.x)*(p1.y - p0.y) - (p1.x - p0.x)*(p2.y - p1.y)) /
		sqrt((p2.x - p1.x)*(p2.x - p1.x) + (p2.y - p1.y)*(p2.y - p1.y));

	// get color
	vec4 color = uColorOuter;
	if (dist < uDistance)
		color = mix(uColorInner, uColorOuter, dist / uDistance);

	// write result
	fragColor = color;
}
```
