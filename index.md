# Context-Aware Web Application: Process Journal

<img src="https://topdevs.org//storage/pictures/0e/b5/0eb534c148ba1f84fdbb4ee629b90d57e2b603e89dd5e5403b8f0a45cf5cf624.5ff30c64.146ab620.jpeg" alt="Geolocation/Top Devs">

## Project Overview
This project is a mobile web application that utilises mobile device sensors (geolocation and device orientation) to create a responsive, context-aware user experience. The app changes its interface and functionality based on the user's location and the orientation of their mobile device.

## Table of Contents
1. [Project Concept & Research](#project-concept-&-research)
2. [Geolocation Integration with Recipe API](#geolocation-integration-with-recipe-api)
3. [Orientation Integration](#orientation-integration)
4. [Combining Location and Orientation](#combining-location-and-orientation)
5. [Refinement](#refinement)
6. [References](#references)

---

## Project Concept & Research

- **Goal**: 
  The primary goal for this was to establish a clear concept for a context-aware mobile web app and explore existing technologies that utilise mobile device sensors (this could be a web interface, viewable on mobile device). The focus was on leveraging geolocation and orientation sensors to provide a personalised, dynamic user experience that adapts to the user's physical environment.

- **Concept**: 
  The app will respond to the user's physical environment by tapping into two key device sensors:
  - **Geolocation (GPS)**: Tracks the user’s position and adapts the app's content based on their location.
  - **Device Orientation (Gyroscope/Accelerometer)**: Tracks how the user is holding or moving their device, altering the app’s behavior accordingly.

### Example Use Cases:
- **Location-based interaction**: The app could display relevant points of interest (e.g., nearby landmarks, cafes, or events) based on the user’s GPS coordinates.
- **Orientation-based interaction**: Depending on the direction the user faces, the app could change the UI or provide context-relevant data, such as showing information about landmarks in the user’s field of view.

### Visual Conceptualisation:
A simple visual representation of the app's key components was created to illustrate how it might work based on sensor input. Below is a conceptual diagram outlining how the geolocation and orientation sensors feed into the app’s interface:

<img src="https://i.imgur.com/or5Akak.png" alt="Geolocation">

- **Inspiration**: 
  - **Research Goal**: Before starting development, I researched existing apps that effectively use geolocation and device orientation sensors. This research helped inform the technical feasibility and design decisions for the app.

  ### Key Inspirations:
  - **Google Maps**: A prime example of geolocation integration. Google Maps continuously updates the user’s position, offering location-based services like navigation, traffic updates, and nearby places of interest.  
    - **Relevance**: Inspired real-time location-based updates in my app.

  - **AR Navigation**: Apps like Google ARCore and Pokémon Go use the phone’s camera and orientation sensors to overlay digital content onto the real world, reacting to how the device is tilted or moved.  
    - **Relevance**: Showcased how orientation-based interactions can enrich the user experience by dynamically adapting the app interface.

  - **Star Walk 2**: This app uses both geolocation and orientation to map out stars based on the user's location and the direction they're pointing their device.  
    - **Relevance**: A strong example of seamlessly integrating geolocation and orientation, providing a model for sensor fusion in my app.

- **Reflection**: 
  Location and orientation sensors offer a simple yet powerful way to create a dynamic, real-world-responsive user experience. However, combining both inputs meaningfully and intuitively presents challenges, such as:
  - Smooth transitions between different interface modes based on location.
  - Responsive, non-intrusive orientation-based actions that feel natural to the user.

### Initial Thoughts:
- **Opportunities**: By merging geolocation and orientation, the app can become a powerful tool for contextual interactions, with potential applications in tourism, education, or navigation.
- **Challenges**: Balancing data from both sensors to provide a fluid experience, handling sensor accuracy, and managing user permissions will be crucial.

### Next Steps:
- Begin prototyping the geolocation feature, focusing on retrieving the user’s position in real time.
- Research sensor fusion techniques to combine orientation and location data for complex interactions.
- Create mockups to visualise how the interface changes with different sensor inputs.


---

## Geolocation Integration with Recipe API

- **Goal**: This week’s goal was to implement geolocation tracking using the `navigator.geolocation` API and integrate it with a Recipe API (e.g., Spoonacular) to suggest context-aware recipes based on the user's location and time of day.

- **Progress**: 
  - **Geolocation Tracking**: Implemented the browser’s `navigator.geolocation` API to fetch the user’s latitude and longitude.
  - **Recipe API Integration**: Integrated the Spoonacular API to fetch recipes based on location, and added a feature to provide meal suggestions depending on the time of day (breakfast, lunch, or dinner).
  - **UI**: The app displays the user’s location and provides recipe suggestions based on local cuisine or regional preferences.
  
  - **Code Snippet**:
    ```javascript
    const apiKey = 'YOUR_API_KEY'; // Your Recipe API Key

    // Get user's current location
    navigator.geolocation.getCurrentPosition(function(position) {
        let latitude = position.coords.latitude;
        let longitude = position.coords.longitude;
        console.log(`Latitude: ${latitude}, Longitude: ${longitude}`);

        // Fetch recipe suggestions based on location and time of day
        const hours = new Date().getHours();
        let mealType = 'dinner'; // Default to dinner
        if (hours < 12) mealType = 'breakfast';
        else if (hours >= 12 && hours < 17) mealType = 'lunch';

        fetch(`https://api.spoonacular.com/recipes/complexSearch?type=${mealType}&apiKey=${apiKey}`)
            .then(response => response.json())
            .then(data => {
                console.log(`${mealType} recipes:`, data);
                // Display recipe results on your web page
            })
            .catch(error => console.error('Error fetching recipes:', error));
    });
    ```

- **Challenges**: 
  - Handling user permission for accessing geolocation data.
  - Testing the accuracy and consistency of location-based recipe suggestions across different devices and regions.
  - Managing API rate limits (due to the free API tier).

- **Reflection**: 
  The integration of geolocation and a recipe API was successfully implemented. By combining the user's real-time location with recipe suggestions, the app enhances the user's experience by providing locally relevant meal ideas. Additionally, incorporating time of day to suggest breakfast, lunch, or dinner was a useful contextual addition. 

  Next steps involve refining the UI and optimizing the performance of API requests. Linking the user’s location more closely with region-specific recipes will further improve the app’s utility.

### Visual Conceptualisation:
I've created a visual representation for Geolocation and Recipe API integration which illustrates how the app might look with geolocation on the top half and recipe suggestions on the bottom half, based on the user's location and time of day:
<img src="https://i.imgur.com/oINXUHo.jpeg" alt="Recipe APP">

### Next Steps: 
  - Improve error handling for cases where geolocation access is denied.
  - Enhance the recipe display by adding images, ingredient lists, and links to detailed instructions.
  - Explore adding more filters, such as dietary preferences or ingredients-based searches.

---

## Orientation Integration
- **Goal**: This week’s objective was to implement device orientation tracking using the gyroscope and accelerometer. I also began exploring ways to combine the orientation data with the geolocation feature introduced earlier. A key application I envisioned is to use these inputs for a kitchen-focused context-aware recipe app, which tailors content based on both the user’s location and orientation within their space.
- **Progress**: 
  - **DeviceOrientation API Integration**: I integrated the DeviceOrientation API to detect changes in the device's rotation (alpha, beta, gamma values), which represent the phone’s orientation in 3D space.
  - **Recipe API Integration**: Using a Recipe API, I plan to dynamically suggest recipes based on the user’s orientation and time of day. For instance, the phone’s orientation could change what is displayed, such as switching between breakfast, lunch, or dinner suggestions when the device is tilted.
  - **UI**: The interface responds to these orientation changes, potentially offering interactive experiences where the user might point their phone in different directions to reveal various recipe ideas.
- **Challenges**:
   - Interpreting orientation data meaningfully and linking it to the user experience was complex. Making sure the content displayed when the user tilts their device feels intuitive, and ensuring that the orientation readings remain accurate without causing confusion.
   - Another challenge was ensuring smooth transitions between geolocation data (e.g., location-based recipe suggestions) and orientation-based UI changes..
- **Code Snippet**:
```javascript
window.addEventListener('deviceorientation', function(event) {
    let alpha = event.alpha; // Rotation around z-axis
    let beta = event.beta;   // Rotation around x-axis
    let gamma = event.gamma; // Rotation around y-axis
    console.log(`Alpha: ${alpha}, Beta: ${beta}, Gamma: ${gamma}`);
    
    // Use orientation to change recipe suggestions
    if (beta > 45) {
        showDinnerRecipes(); // Tilted forward, show dinner options
    } else if (beta < -45) {
        showBreakfastRecipes(); // Tilted backward, show breakfast options
    } else {
        showLunchRecipes(); // Neutral, show lunch options
    }
});
 ```
- **Reflection**: 
  The orientation integration adds an exciting layer of interactivity. I see great potential in combining geolocation with orientation, particularly for an app that adapts to user behaviors like moving around the kitchen, pointing their phone towards different areas, and receiving recipe suggestions accordingly. A key challenge moving forward will be to ensure that orientation-based transitions feel smooth and purposeful without overwhelming the user with too many sudden UI changes.

### Visual Conceptualisation:
I created a simple diagram to show how the app uses both geolocation and device orientation to tailor recipe suggestions for users in a kitchen environment.
<img src="https://i.imgur.com/TfQdArb.jpeg" alt="Recipe APP">

### Next Steps: 
- Continue refining how geolocation and orientation inputs work together to create a seamless and intuitive user experience.
- Experiment with more practical use cases in the kitchen context. For instance, tying the Recipe API to seasonal ingredients or nearby grocery store locations based on the user's current geolocation.
- Explore further customization for recipe suggestions by linking orientation with the time of day, weather, and user preferences.

---

## Combining Location and Orientation
- **Goal**: Merge geolocation and orientation functionality to create a seamless user experience.
- **Progress**: 
  - Successfully combined location and orientation tracking.
  - Developed a feature where the app provides different information based on the user's location and device tilt.
  - Example: The app now shows nearby landmarks based on location and adjusts UI content based on the phone’s direction.
- **Challenges**: Ensuring that changes in orientation feel intuitive and not overwhelming, while handling location updates efficiently.
- **Reflection**: Combining these two sensors results in a richer, more immersive experience. Testing in different environments will be crucial for optimization.

---

## Refinement
- **Goal**: Improve UI/UX and handle edge cases.
- **Progress**: 
  - Refined the app’s design to ensure smooth transitions between different contexts (location changes and orientation shifts).
  - Implemented error handling for cases where users deny sensor permissions or move to areas with poor GPS signal.
  - Conducted user testing to gather feedback.
- **Next Steps**: Prepare for the final project presentation, refine edge cases, and ensure cross-browser compatibility.

---

## References:

### Geolocation API Documentation
- **Description**: Provides real-time location information, including latitude, longitude, altitude, and accuracy, from the user's device.
- **Use Case**: Used to fetch the user's current geographic position in the web app.
- **Link**: [Geolocation API Documentation](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API)

### DeviceOrientation API Documentation
- **Description**: Allows access to the orientation of the user's device (alpha, beta, gamma values) relative to the Earth’s frame of reference.
- **Use Case**: Implemented to detect and react to changes in the device's rotation in the web app.
- **Link**: [DeviceOrientation API Documentation](https://developer.mozilla.org/en-US/docs/Web/API/DeviceOrientationEvent)

### Google Maps API Documentation
- **Description**: Provides a map interface and related services, such as displaying maps, routes, and points of interest.
- **Use Case**: Integrated to display the user's real-time location and provide contextual map data based on geolocation.
- **Link**: [Google Maps API Documentation](https://developers.google.com/maps/documentation)

### Similar Projects and Inspiration
- **Description**: Research and inspiration from existing projects and tools that leverage geolocation, orientation sensors, and context-aware web apps.
- **Link**: [Similar Projects and Inspiration](#) (Add your relevant links here)

---

### Highlights:
- The document is formatted clearly with proper headings for each section.
- Includes a reflection for each week, outlining the insights gained.
- The code snippets and technical challenges are clearly documented.
- References are linked for easy access to documentation.





