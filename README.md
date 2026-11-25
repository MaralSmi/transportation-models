# Transportation Planning Models

Six interactive calculators developed for a transportation planning course. They cover three questions that come up when studying travel demand: where trips go, which mode travelers choose, and how traffic divides between routes. Each calculator runs in the browser and shows the intermediate calculations so you can compare the results with a hand-worked solution.

## Getting started

Download and extract the repository, then open `index.html` in a browser. The Persian landing page links to all six calculators, which have English interfaces. Each HTML file contains its own form, styles, and calculation code. You can also open a calculator directly. Keep the HTML files together in the same directory so the landing page links work.

Start with the values already entered in a calculator and run it once. Then change one input and run it again. Comparing the two reports makes it easier to see which part of the calculation responds to that change.

## Choosing a calculator

| If your question is… | Use this calculator |
| --- | --- |
| Where will trips from each origin go, given the attractiveness and travel impedance of each destination? | [Gravity model](gravity_model.html) |
| How might an existing pattern of trips change as different zones grow? | [Fratar growth-factor model](furness_model.html) |
| How many daily trips will use a private car or a bus, given their travel characteristics? | [Binary logit](logit_model.html) |
| How will existing auto, bus, and rail shares change after a service adjustment? | [Incremental multinomial logit](multinomial_logit_model.html) |
| How do time, income, and out-of-pocket costs affect the split between auto and transit? | [Quick Response System (QRS)](QRS_model.html) |
| How does a change in route travel time affect the next allocation of traffic? | [TRC route assignment](TRC_model.html) |

## Trip distribution

### Gravity model

The gravity calculator distributes trips among four zones. Enter each zone’s trip productions and attractions, the travel impedance between zones, the impedance exponent, and the socioeconomic adjustment factors. A production is a trip originating in a zone. An attraction is a trip drawn to a destination.

For each origin, the model weights the available destinations by attraction, inverse-power impedance, a socioeconomic factor, and a destination balancing factor. It divides the origin’s trips among destinations in proportion to those weights. After an allocation, the calculator compares the estimated arrivals with the attraction targets and updates the balancing factors. The report shows the impedance factors, allocations, and destination checks. For a balanced exercise, choose productions and attractions with the same grand total.

### Fratar growth-factor model (Furness page)

This calculator starts from an observed pattern of travel between two to eight zones. Enter the base trip total and growth factor for each zone, then fill in one half of the interzonal trip matrix. The form mirrors the entries across the diagonal. Each zone’s target equals its base total multiplied by its growth factor.

At each iteration, the calculator estimates trips in both directions for each zone pair and averages the two estimates to preserve symmetry. It sums the revised rows and divides each target by its revised total to get the next growth factor. A factor of 1 means that zone has reached its target. The final matrix and convergence history show how close all zones came before the tolerance or iteration limit was reached.

## Mode choice

### Binary logit

The binary logit calculator compares private car and bus for a specified number of daily trips. Each mode has its own constant and values for access time, waiting time, travel time, and monetary cost. The four coefficients describe how those attributes contribute to utility.

The calculator exponentiates each mode’s utility and divides by the sum for both modes to obtain its choice probability. Multiplying that probability by daily demand gives the estimated trip count. For a simple experiment, reduce bus waiting time from the default 15 minutes to 5. With the default waiting-time coefficient of −0.032, bus utility increases by 0.32. The report shows how that improvement changes bus share and ridership.

### Incremental multinomial logit

Use this calculator when starting shares are available for auto, bus, and rail. Enter those shares as fractions that sum to 1, together with old and new travel and waiting times. The calculator measures the change in utility for each mode and uses it to update the baseline shares.

For mode *k*, the weight is its initial share multiplied by the exponential of its utility change. The new share is that weight divided by the sum of all three weights. In the supplied example, bus waiting time rises from 3 to 4 minutes while rail waiting time falls from 10 to 7.5 minutes. Auto’s own inputs stay fixed, but its share can still change because all three modes share the same denominator.

### Quick Response System (QRS)

The QRS calculator estimates auto and transit shares from travel impedance. Inputs include annual income, annual working minutes, total trips, a sensitivity exponent, and each mode’s distance, speed, excess time, cost per kilometer, and parking charge.

Distance and speed determine in-vehicle minutes. The calculator weights excess time by 2.5 and converts monetary cost to equivalent minutes using income per working minute and a multiplier of 3. It includes half the entered parking charge in the one-way trip cost. The report shows both impedance calculations, the resulting mode shares, and the trips assigned to each mode. With a positive sensitivity exponent, increasing a mode’s impedance reduces its share.

## Route assignment

### TRC model

The TRC calculator assigns a specified traffic volume between two competing routes. Enter the route lengths, initial travel-time rates, reference time rates and volumes, and the number of iterations. Initial route time equals the starting time per unit of distance multiplied by route length.

Each iteration allocates volume in proportion to the reciprocal of the current route time. A shorter travel time therefore attracts more traffic in that iteration. The calculator rounds the assigned volumes, then updates each route’s travel time according to its volume relative to its reference volume. The update uses a coefficient of 0.5 below the reference volume and 10 at or above it. From the second iteration onward, the report gives the absolute change in each route’s time in minutes and seconds. The run ends after the selected number of iterations, so the reported changes are useful for judging whether the times have settled.
