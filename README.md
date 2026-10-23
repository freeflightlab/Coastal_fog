Sea cliff and bay air tools
Illustrated README and user guide
These four standalone HTML tools explore how temperature, humidity, fog, wind and coastal terrain affect air density, aerodynamic force and rising air. Start with the density calculator, use the lift calculator to understand the mechanisms, then use Sea Cliff Flow to explore their spatial and time-dependent behavior.
Choose the right file

Open and use the tools
Save the HTML files to your computer and open one in a modern browser. Calculations run in the page; the flow tools also use a background worker. No installation or account is required. The files reference Google Fonts, so offline use may substitute local fonts. Browser or embedded-preview restrictions can affect clipboard, downloads or workers; opening the downloaded file directly is the first troubleshooting step.
For a first pass, choose an example, change one input, and compare the result with the original. In the flow tools, allow simulated time to advance before interpreting the solution. Keep the HTML version with any saved setup so another person can reproduce the calculation.
Scope of this guide
Prepared from the four supplied HTML files and four supplied screenshots. Pictures show illustrative saved states from October 14, 2026; they are not measurements or proof of solver accuracy. This guide explains the implementation and its built-in checks; it does not independently validate the models. The HTML tools are unchanged.
Bay air density
Use bay-air-density_tool.html to isolate the effects of temperature, moisture and pressure before adding terrain or buoyancy. The density dial compares the current air with standard dry air at 59°F and 29.92 inHg, approximately 1.225 kg/m³.

Figure 1  Cold clear air example from the supplied screenshot. The density is 1.277 kg/m³, giving 4.3% more aerodynamic force at the same speed.
Set conditions and read the result
Set Air temperature, Relative humidity and Barometer, then set Wind speed. The secondary labels show converted units, dew point and water-vapor content. Example air buttons provide quick comparisons, including Summer fog, Hot fall day, Winter storm and Cold clear high. Copy this reading copies a textual summary.
At fixed speed and shape, force changes directly with density. The screenshot’s 15 kn wind has the same dynamic pressure as approximately 15.3 kn in standard air. This is a force-equivalent speed, not a change in the actual wind speed.
What the sail number means
The displayed force uses a flat plate facing the wind with coefficient 1.28. It is an illustrative load on the stated area, not a sailboat performance prediction. A working sail has lift and drag that depend on angle, trim and apparent wind.
Density comparisons and fog

Figure 2  Hot air example at 86°F, 30% relative humidity and 29.92 inHg. At 15 kn, the tool shows 1.159 kg/m³ and 5.4% less force than standard air.
Why the two examples differ
Temperature, humidity and pressure all change between Figures 1 and 2. Their difference cannot be attributed to humidity alone. To isolate an effect, hold two inputs fixed and sweep the third. Water vapor lowers gas density at fixed temperature and pressure because it replaces heavier dry-air molecules.
The tool uses ρ = (p − e)/(Rd T) + e/(Rv T), with absolute temperature T, total pressure p and vapor pressure e. Wind loading uses q = ½ρV² and F = q Cd A. The force-equivalent standard-air speed is V √(ρ/1.225). Doubling wind speed therefore quadruples the load at fixed density.
Explore the lower sections
Momentum and the force plot show how speed and density affect loading. The temperature and humidity plots and Density table show broader comparisons. Evaporating fog adds liquid water to an air sample and solves an approximately constant-pressure, adiabatic enthalpy balance: evaporation consumes heat, cools the air and increases humidity. The available water and saturation limit how much can evaporate.
Fog droplets and water vapor are different quantities. Do not interpret 100% relative humidity as a specified liquid-water content. Use the built-in reference table to inspect formula comparisons; agreement on density or vapor pressure does not validate real sail loads or local weather.
Sea cliff lift
Use sea-cliff-lift_tool.html for a quick explanation of why a cliff might produce rising air. It combines a prescribed airflow slope with a lifted parcel, environmental stability, humidity, condensation, solar heating and a density correction to wing sink.

Figure 3  Example cliff-top budget. The displayed +0.73 m/s is an optimistic model net climb after subtracting wing sink. The chart shares interacting buoyancy effects among humidity, fog and sunshine.
A practical input sequence
1. Set beach temperature, humidity and barometer. 2. Set cliff-top wind, angle off straight in and cliff height. 3. Choose the slope the airflow follows and your wing’s standard-air minimum sink. 4. Set the environmental lapse rate, humidity at cliff-top height and inversion. 5. Adjust Sun heating the air and compare the budget.
The airflow slope is rise divided by horizontal run; it is not the rock-face angle. A slope of 1:4 means a rise/run ratio of 0.25. The Sun heating the air input is a sensible heat flux into the air, not the full incoming sunlight at the ground.
Read the budget carefully
Ridge lift is the forced vertical component of wind. Stable air can reduce it. The parcel model then adds positive buoyancy effects and subtracts wing sink. Fog on the face estimates where the parcel saturates; Top of the lift estimates an idealized stopping height. The separate thermal estimate describes additional localized heating potential, rather than a continuous climb available everywhere.
How the lift model works
Wind and terrain
The incoming normal wind is Uin = U cos(α). For an airflow rise/run slope s, the unblocked ridge estimate is wr = Uin s/√(1 + s²). Oblique wind reduces the component entering the face. Stable cases use a bulk Froude-number approximation, Fr = Uin/(NH), to reduce forced lift when Fr is below one.
Humidity and condensation
A beach-air parcel cools as it rises. Before saturation it follows an approximately dry adiabatic rate; after saturation, latent heat release slows its cooling. The surrounding air follows the chosen environmental lapse rate. The model compares parcel and environmental density, including lighter water vapor and the loading from liquid droplets.
Positive parcel buoyancy is integrated as energy and converted to an idealized speed gain. Negative buoyancy limits the rise above the crest rather than simply removing all wind-forced uplift on the face. The model neglects entrainment, so buoyancy-enhanced results are upper estimates. Mixing with the surroundings can substantially reduce the gain.
Why the colored bars are not separate experiments
Humidity, condensation and heating interact. The calculator uses Shapley values: it evaluates combinations of these effects and averages their incremental contributions over possible addition orders. The bars sum to the calculated total, but are an attribution convention rather than independently measurable velocities.
Wing sink and stability
Minimum sink is scaled approximately by √(1.225/ρ) at cliff-top conditions. Net climb is the modeled air rise minus that corrected sink. This assumes comparable flight conditions and does not include a full wing polar, turns or pilot control. A positive value does not demonstrate usable or safe lift.
A larger positive environmental lapse rate means faster cooling with height; a negative value means warming with height. An inversion acts as a stable lid. Humidity differences can also change buoyancy, so a temperature-only stability label does not tell the whole story.
Useful comparisons
Run Fog on the face, drier above against Inside a fog bank to examine condensation and moisture contrasts. Compare Sunny, dry aloft with Low inversion lid to see how heating and a cap affect the outcome. Change only one control after each preset. The model excludes resolved turbulence, rotor, vertical wind shear and three-dimensional cliff geometry.
Sea Cliff Flow
Sea-Cliff-Fl.html and Sea-Cliff-Fl_extend.html calculate evolving wind, moisture and heat on a vertical grid. They include a transported along-coast velocity component, which makes them 2.5D slice models. The coast view arranges independent solutions in space; it is not a fully coupled three-dimensional CFD domain.

Figure 4  Along the coast view from the supplied screenshot. Slices have separate solutions; particles can drift between their displayed fields. The picture uses vertical exaggeration, marked Heights ×2.
Run a first simulation
Choose Examples or keep the initial setup. Confirm the wind reference height and direction, air profile, inversion, sea temperature and cliff shape. Choose Medium grid, press Run, and let the simulated clock advance. Pause to inspect the field; tap the slice to move the probe, drag to pan and use the zoom controls to reframe it.
Geometry and grid changes rebuild the simulation. Other condition changes can modify an evolving run; for a controlled comparison, use Restart and compare at similar simulated times. A running animation alone does not establish that the result has settled.
Flow fields and terrain
Use the maps together

Load a real terrain line
Select Load a terrain profile or drop a GPX, KML, GeoJSON or CSV file onto the page. Supply elevations along a line from water inland across the cliff. Supported CSV forms include distance/elevation and latitude/longitude/elevation. A geographic line without elevations cannot supply the cliff shape. Inspect the preview, elevation units, sea end and coast orientation before choosing Use this profile for the slice.
The manual profile editor uses feet for displayed distance/elevation pairs, while saved JSON uses SI units. The importer can infer the sea from the lower endpoint; verify this on uneven inland terrain. Review where the tool locates the shore and crest rather than assuming automatic detection matches the site.
Build a stretch of coast
Use Add a slice here or Copy to the north, edit each geometry, and select Solve every slice. Moving between slices can interpolate geometry at intermediate positions. Compare results at similar simulated ages. Changing coast length alters a parameterized sideways drainage of blocked marine air; actual gaps and headlands are not explicitly solved in three dimensions.
Extended features and reproducibility
What the extended file adds
Sea-Cliff-Fl_extend.html adds Fog through time, seen from above beneath the main slice. It is a distance–time history with newest samples at the top, aligned horizontally with the slice. Shading represents a fog-reflectance proxy; hatching indicates fog reaching the ground. This is a model visualization, not satellite imagery or an along-coast map.
Where the sunshine on the land goes traces reflected sunlight, absorption in fog, energy reaching the ground and subsequent surface pathways. Read it alongside Energy and water in the slice, whose budgets use the last minute of simulated time and are normalized by the modeled ground area, excluding the held-inflow strip. Fog water totals in kg/m are per unit along-coast width, not a whole-coast inventory.
The extension also changes the incoming sounding treatment when the inversion is off, adjusts sounding saturation handling and adds a sea vapor-flux configuration option. These are physics changes as well as display additions: the same saved setup can give different results between the two flow files.
Save and exchange a study
Use Copy JSON to expose or copy the configuration; Open .json loads it. Save .json, the slice picture button and Download the tool (.html) may appear where the browser supports them. If downloads are unavailable, copy the configuration text into a .json file. The flow schema identifies format sea-cliff-flow and version 1 and stores air, wind, surface, fog, domain and slice settings.
JSON saves a setup, not a restart checkpoint containing the evolved velocity and fog fields. Keep the exact HTML file, JSON setup, simulated time, grid, probe position and result images together. After reloading, rerun the simulation. The density and simplified lift calculators do not share the flow configuration schema; transfer comparable input values manually.
Check results before drawing conclusions
Compare Medium and Fine grids at the same physical position and similar simulated ages. The tool’s own notes report greater sensitivity within about 50 ft of the ground. Watch probe and budget histories for continuing drift. Run the flow checks again if needed: some benchmark values are stored from the build, while thermodynamic and optical checks are computed live. Formula checks and standard test shapes do not establish accuracy for your specific cliff and fog case.
The solver uses finite volumes, Boussinesq flow, pressure projection and a k–ε turbulence closure. It averages turbulence and individual thermals; terrain is represented by blocked Cartesian cells. Important omissions include fully coupled along-coast pressure effects, resolved gusts, drizzle and larger weather systems. Use the results to compare mechanisms and sensitivities, not as a flight forecast.
Troubleshooting and source references
If a run is slow, switch to Coarse or Medium and solve fewer slices. If it will not start, open the standalone HTML in a browser that permits workers. Check units and profile orientation for implausible terrain or lift. Clipboard failure can be bypassed by manually selecting the JSON text. Browser storage is convenient but is not a substitute for an exported setup.
Each HTML contains its own method notes, benchmark tables and linked references. Principal sources cited there include CIPM-2007 and IAPWS for moist-air properties, NASA Glenn for aerodynamic scaling, FAA ridge-soaring guidance, and Bolund, DYCOMS-II, Slingo and delta-Eddington references for the flow and fog model. Consult those in-page links for the exact source associated with a calculation.
