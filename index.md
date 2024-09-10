# Context-Aware Web Application: Process Journal

## Project Overview
This project is a mobile web application that utilizes mobile device sensors (geolocation and device orientation) to create a responsive, context-aware user experience. The app changes its interface and functionality based on the user's location and the orientation of their mobile device.

## Table of Contents
1. [Week 1: Project Concept & Research](#week-1-project-concept--research)
2. [Week 2: Geolocation Integration](#week-2-geolocation-integration)
3. [Week 3: Orientation Integration](#week-3-orientation-integration)
4. [Week 4: Combining Location and Orientation](#week-4-combining-location-and-orientation)
5. [Week 5: Refinement](#week-5-refinement)
6. [References](#references)

---

## Week 1: Project Concept & Research
- **Goal**: Establish a concept for a context-aware app and research similar projects.
- **Concept**: The app will respond to the user's physical environment, using mobile device sensors such as location (via GPS) and orientation (via gyroscope/accelerometer).
- **Inspiration**: Explored apps such as Google Maps for geolocation and augmented reality apps for orientation tracking.
- **Reflection**: Location and orientation sensors offer a simple yet powerful way to create a dynamic, real-world-responsive user experience. The challenge will be combining both inputs meaningfully.

---

## Week 2: Geolocation Integration
- **Goal**: Implement geolocation to track the user’s location and provide real-time information.
- **Progress**: 
  - Used the browser's built-in `navigator.geolocation` API to fetch latitude and longitude.
  - Integrated **Google Maps API** to display the user’s current location on a map.
- **Challenges**: Handling cases where users deny location access and testing accuracy in different environments.
- **Code Snippet**:
  ```javascript
  navigator.geolocation.getCurrentPosition(function(position) {
      let latitude = position.coords.latitude;
      let longitude = position.coords.longitude;
      console.log("Latitude: " + latitude + ", Longitude: " + longitude);
      // Display location on map
  });
Reflection: The geolocation feature was successfully implemented. Next, I plan to link this location data to real-time contextual information, such as nearby points of interest.

Week 3: Orientation Integration
Goal: Implement device orientation tracking using the gyroscope and accelerometer.
Progress:
Integrated the DeviceOrientation API to detect changes in device rotation.
Tested UI reactions to different device orientations.
Challenges: Interpreting orientation data meaningfully (alpha, beta, gamma values) and providing a smooth user experience.
Code Snippet:
javascript
Copy code
window.addEventListener('deviceorientation', function(event) {
    let alpha = event.alpha;
    let beta = event.beta;
    let gamma = event.gamma;
    console.log(`Alpha: ${alpha}, Beta: ${beta}, Gamma: ${gamma}`);
});
Reflection: This feature can create a fun and interactive experience, such as changing information displayed based on which direction the user is facing.
Week 4: Combining Location and Orientation
Goal: Merge geolocation and orientation functionality to create a seamless user experience.
Progress:
Successfully combined location and orientation tracking.
Developed a feature where the app provides different information based on the user's location and device tilt.
Example: The app now shows nearby landmarks based on location and adjusts UI content based on the phone’s direction.
Challenges: Ensuring that changes in orientation feel intuitive and not overwhelming, while handling location updates efficiently.
Reflection: Combining these two sensors results in a richer, more immersive experience. Testing in different environments will be crucial for optimization.
Week 5: Refinement
Goal: Improve UI/UX and handle edge cases.
Progress:
Refined the app’s design to ensure a smooth transition between different contexts (location changes and orientation shifts).
Implemented error handling for cases where users deny sensor permissions or move to areas with poor GPS signal.
Conducted user testing to gather feedback.
Next Steps: Prepare for the final project presentation, refine edge cases, and ensure cross-browser compatibility.
References
Geolocation API Documentation
DeviceOrientation API Documentation
Google Maps API Documentation
[Similar Projects and Inspiration](links to relevant project research)
vbnet
Copy code

### Key Points in the Markdown:
- **Week-by-week structure** that documents both the technical and conceptual aspects of your development.
- **Code snippets** to show your progress on integrating geolocation and orientation.
- **Reflection sections** to discuss your insights and challenges, helping you track how your understanding evolves.

Let me know if you’d like further customization or any additions!






