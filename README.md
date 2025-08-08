# U1PhaseField-NodeRepulsion
Background HTML GUI -High CPU- BETA


The background color is driven by a phase value. That phase comes from adding two moving, slanted waves. Think of each wave like evenly spaced stripes sliding over time. You add their directions as complex numbers, then take the compass angle of the result. That angle runs from 0 to a full turn.

We convert this angle into a light wavelength. Then we wiggle the wavelength a little with a slow sine. A small wiggle avoids harsh color jumps. We clamp to the visible range so it never goes out of gamut. A piecewise function turns wavelength into RGB. A gamma curve brightens darker primaries to look right on screens. Edge wavelengths get lower alpha to mimic how human eyes see less near the extremes.

Nodes move by following a direction pulled from Perlin noise. Noise makes smooth changes in space and time. So heading changes are gentle, not jittery. Each step adds a small steering push, caps the speed, and wraps around the screen. Near the mouse, nodes get a shove away that fades with distance. Links appear between nodes that are close. Line opacity and thickness fade with distance. That makes nearby pairs look stronger. NOTE: CPU USAGE HIGH. 

The “cosmic” particles ride a separate flow. We build a coarse grid of flow angles from two octaves of Perlin noise. Two octaves add large shapes plus finer swirls. Angles are scaled to a full circle. The grid evolves by moving the noise's Z slice forward a bit each frame. Each particle samples the four nearest grid cells and blends their angles. Bilinear interpolation.

Particles feel a constant push along the local flow angle. If the mouse is pressed, they also feel a pull toward the cursor. The pull strength drops as 1/(distance+1). Motion uses simple Euler integration with damping, a speed cap, and torus wrapping. Every frame (lowered from 4000 to 400), we draw tiny, translucent dots in additive mode. A very faint black fill erases slowly (bug noted), leaving trails. The palette cycles five hues around the color wheel, spaced evenly, so the trails vary without clashing.

The cursor ring reads the same phase field as the background, but in a redder wavelength range. Two rings with different line widths and alphas should create a crisp core and a soft halo.
