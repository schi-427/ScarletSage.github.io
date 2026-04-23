---
layout: post
title: Greenspace Project Update
date: 2026-04-23
category: Programming
permalink: /blog/greenspace-map-2/
---
I've made a decent amount of progress since my last post. As expected, continuing to read the literature around greenspace accessibility has given me a great deal of insight. 
For the purposes of this post, I'll focus on this paper from Swansea University's Sarah Nicholls:

[Measuring the accessibility and equity of public parks: A case study using GIS](https://www.researchgate.net/publication/35504885_Measuring_the_accessibility_and_equity_of_public_parks_A_case_study_using_GIS)

This paper does a great job of explaining the different methods and schools of thoughs behind determining greenspace access. 
As Nicholls points out, the [National Recreation and Park Association/NRPA](https://www.nrpa.org/) sets a target metric (or at least did when the paper was written) of 10 acres of open space per 1000 residents in a city. 
This serves as a decent general benchmark, but many cities go a bit deeper, dividing their urban areas into smaller zones and then calculating the metrics of these zones. 
Either way, Nicholls points out important drawbacks to this ratio method:
- It assumes that the benefits of services are allocated only to residents in the predefined zone(s) in which they lived, and that no spatial externalities in the sorrounding areas occur, which is not always the case.
- It assumes that people in an area have enough access so that they all benefit from the services provided, which is not always the case.
- It does not consider spatial distribution of opportunities, whereas the location of the parks relative to their potential users seems important if we're trying to determine accessibility and equity.

Therefore, more complex formulas are nedeed to be better determine access. Nichols also discusses a "radius method", where a centroid of each park is determined, and then a circle is established
around these, theoretically getting the park's total service area. The radius of the circle is the maximum desired distance of userse from it, as determined by the city. Residents are considered covered if they fall within the circle. 
This method is better, in that it considers spatial factors, but is not perfect, as Nichols points out:
- This only provides an approximate representation of a service area, since it uses "as the crow flies" movement. The reality of how park users get to parks is much more complex. Instead, they move along predefined pathways. This means the actual travel distance is probably underestimated, and the service area is overestimated in this method.
- It assumes that the park is accessible from all sides, when this is often not true and many parks have specific entry points. This can also lead to an overestimation of service area, as the true path to enter is underestimated.
- The use of a centroid as the center of the access area could lead to underestimation in large parks. The larger a park is, the more of its own space might occupy the service area circle.

So while this method is better, it has clear downsides. Nicholls recommends a third method rooted in network analysis that measures the distance along walkable roads and other public rights of way around the parks, emulating the actual routes that users are likely to follow between their residences and park entry points. 
This can be done in GIS via shortest path algorithms. 

So while the network analysis will be my ultimate goal, I think it's helpful to start smaller, with the simple ratio calculations. I think these measurements are still valuable as a general high-level greenspace access metric, even if it's lacking in the areas described above. 
I took the following steps to get these measurements:

1. Combined my county recreation complexes layer with my county+city parks layer.
2. Created a 1000 meter buffer layer around the city limits, the idea being that I should make sure to catch any greenspace that is not in the city but still accessible to city residents.
3. Selected the parks and complexes that intersected with my buffer layer, saving these as a new layer.
4. Used the stats function in QGIS to determine the total area of parks and complexes, which was 619,900 meters squared, or 153.18 acres.
5. Using the estimated population of the city from Google, this is 29,656.
6. To find the ratio, divide the acreage, 153.18 by the population, 29,656, and multiply this number by 1000 to get 5.1652.

**This falls well below the NRPA's ideal space metric 10 acres of space per 1000 residents.**

<img width="700" height="800" alt="Screenshot 2026-04-23 122249" src="https://github.com/user-attachments/assets/0e6a083a-1f8a-4889-92e3-dff084adcb25" />


For the sake of thoroughness, I also wanted to consider recreational trails. Horry County has various recreational trails, and a few of these are near Conway, aside from the trails Conway itself has. So to get the caclulations with the trails included:
1. Since the trails were initially line-based layers, I needed to convert them to polygons to get the area. I used the QGIS buffer feature to generate 20m buffers around the trails, saving this as a new layer.
2. Combined this layer with the complexes and parks layer, using the field calculator to popualate the trail entries with area data, and then also for acreage.
3. Created a dissolved layer from this that combines all entires into one entity, this way avoiding any potential overlaps.
4. This time the sum acreage was 675.308, far more than the parks and complexes acreage alone.
5. The ratio worked out to 22.771, a 340.88% increase from the other figure.

<img width="728" height="627" alt="Screenshot 2026-04-23 122738" src="https://github.com/user-attachments/assets/958b3e10-472d-460f-aa47-1038a151b008" />

Looking at the map, this is execpted, considering the length of the nearby trails. In particular, the trail in the circle below is one long bike trail, much of which actually shares roads and highways. 

<img width="700" height="800" alt="Screenshot 2026-04-23 123333" src="https://github.com/user-attachments/assets/9fdef811-6d68-47e5-9d99-8f07a65225ec" />

So while it's clear there is a lot of trail area, I don't think this is paricularly helpful for a gresnspace access study. I'm not sure the trails should be considered "open green space" to the degree actual parks are, so while I can have this data
as a helpful supplement, I don't think it should be the main focus. Going forward, as I move to my "radius" and  "road network" analyses, I will not factor in the trails data except as a supplement. 

Overall, I feel very happy with my progress on this project, and I think I'm in the ideal place to continue with my analysis. I've updated my project map with the new layers here: (https://schi-427.github.io/horry-county-gis/#12/33.8573/-79.0094)
