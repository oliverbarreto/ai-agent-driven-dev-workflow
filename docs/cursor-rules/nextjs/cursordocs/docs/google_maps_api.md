---
title: "Creating an Interactive Map with the Google Maps API in Next.js"
source: "https://dev.to/adrianbailador/creating-an-interactive-map-with-the-google-maps-api-in-nextjs-54a4"
published: 2024-06-08
description: "Introduction   In this article, we will learn how to integrate the Google Maps API into a... Tagged with webdev, javascript, nextjs, googlecloud."
---

# Creating an Interactive Map with the Google Maps API in Next.js

## Introduction

In this article, we will learn how to integrate the Google Maps API into a Next.js application. We will cover everything from the initial setup to implementing advanced features such as multiple markers, routes, and calculating distances between locations.

## Step 1: Initial Setup of the Next.js Project

First, let's create a new Next.js project. Open your terminal and run the following commands:

```shell
npx create-next-app my-google-maps-app
cd my-google-maps-app
npm install --save @react-google-maps/api
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

## Step 2: Obtain the Google Maps API Key

1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. Create a new project or select an existing one.
3. In the navigation menu, go to `APIs & Services > Library`.
4. Search for "Maps JavaScript API" and click on it.
5. Click `Enable` to activate the API for your project.
6. Go to `APIs & Services > Credentials`.
7. Click `Create credentials` and select `API key`.
8. Copy the generated API key. This is the key you will use in your code.

## Step 3: Handling Environment Variables in Next.js

Use environment variables to avoid exposing your API key in the source code. Create a `.env.local` file in the root of your project and add your API key:

```
NEXT_PUBLIC_GOOGLE_MAPS_API_KEY=your_api_key_here
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

## Step 4: Create a React Component with a Google Map

Here's an example of how to use the Google Maps API in a React component to display a map with a marker:

```jsx
"use client"
import React from "react"
import { GoogleMap, LoadScript, Marker } from "@react-google-maps/api"

const containerStyle = {
  width: "100%",
  height: "400px"
}

const center = {
  lat: 37.437041393899676,
  lng: -4.191635586788259
}

const GoogleMapComponent = () => {
  return (
    <LoadScript googleMapsApiKey={process.env.NEXT_PUBLIC_GOOGLE_MAPS_API_KEY}>
      <GoogleMap mapContainerStyle={containerStyle} center={center} zoom={10}>
        <Marker position={center} />
      </GoogleMap>
    </LoadScript>
  )
}

export default GoogleMapComponent
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

## Step 5: Add Routes to the Map

To add routes to the map, you must use the `DirectionsService` and `DirectionsRenderer` components from the `@react-google-maps/api` library. Here's an example of how to do this:

```jsx
"use client"
import React from "react"
import {
  GoogleMap,
  LoadScript,
  Marker,
  DirectionsService,
  DirectionsRenderer
} from "@react-google-maps/api"

const containerStyle = {
  width: "100%",
  height: "400px"
}

const origin = {
  lat: 37.437041393899676,
  lng: -4.191635586788259
}

const destination = {
  lat: 37.440575591901045,
  lng: -4.231433159434073
}

const GoogleMapRouteComponent = () => {
  const [directions, setDirections] = React.useState(null)
  const [travelTime, setTravelTime] = React.useState(null)

  const directionsCallback = (response) => {
    if (response !== null) {
      if (response.status === "OK") {
        setDirections(response)
        const route = response.routes[0].legs[0]
        setTravelTime(route.duration.text)
      } else {
        console.error("Directions request failed due to " + response.status)
      }
    }
  }

  return (
    <LoadScript googleMapsApiKey={process.env.NEXT_PUBLIC_GOOGLE_MAPS_API_KEY}>
      <GoogleMap mapContainerStyle={containerStyle} center={origin} zoom={10}>
        <Marker position={origin} />
        <Marker position={destination} />
        <DirectionsService
          options={{
            destination: destination,
            origin: origin,
            travelMode: "DRIVING"
          }}
          callback={directionsCallback}
        />
        {directions && (
          <DirectionsRenderer
            options={{
              directions: directions
            }}
          />
        )}
      </GoogleMap>
      {travelTime && <p>Estimated travel time: {travelTime}</p>}
    </LoadScript>
  )
}

export default GoogleMapRouteComponent
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

## Step 6: Explanation of the Directions API

The Google Maps Directions API is a service that calculates directions between locations. It can provide detailed route information, including travel time, distance, and steps for navigating from one place to another. In the above example:

- **DirectionsService**: This component is used to fetch directions from the Google Maps API. It requires options such as the origin, destination, and travel mode (e.g., driving, walking, biking).
- **DirectionsRenderer**: This component takes the directions fetched by the `DirectionsService` and renders them on the map.
- **Callback Function**: The callback function processes the response from the Directions API. If the response is successful (`status === 'OK'`), it updates the state with the directions and the travel time.

## Step 7: Add a Loader While the Map is Loading

To improve the user experience, you can add a loader while the map is loading:

```jsx
// components/Loader.js
const Loader = () => (
  <div
    style={{
      display: "flex",
      justifyContent: "centre",
      alignItems: "centre",
      height: "400px"
    }}
  >
    <p>Loading...</p>
  </div>
)

export default Loader
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

```jsx
"use client"
import React from "react"
import { GoogleMap, LoadScript, Marker } from "@react-google-maps/api"
import Loader from "../components/Loader"

const containerStyle = {
  width: "100%",
  height: "400px"
}

const centre = {
  lat: 37.437041393899676,
  lng: -4.191635586788259
}

const GoogleMapComponent = () => {
  return (
    <LoadScript
      googleMapsApiKey={process.env.NEXT_PUBLIC_GOOGLE_MAPS_API_KEY}
      loadingElement={<Loader />}
    >
      <GoogleMap mapContainerStyle={containerStyle} centre={centre} zoom={10}>
        <Marker position={centre} />
      </GoogleMap>
    </LoadScript>
  )
}

export default GoogleMapComponent
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

## Step 8: Implementing Multiple Markers

To display multiple locations on the map, you can iterate over an array of locations and create a marker for each one.

```jsx
"use client"
import React from "react"
import { GoogleMap, LoadScript, Marker } from "@react-google-maps/api"

const containerStyle = {
  width: "100%",
  height: "400px"
}

const centre = {
  lat: 37.437041393899676,
  lng: -4.191635586788259
}

const locations = [
  { lat: 37.437041393899676, lng: -4.191635586788259 },
  { lat: 37.440575591901045, lng: -4.231433159434073 }
  // Add more locations here
]

const MultipleMarkersMap = () => {
  return (
    <LoadScript googleMapsApiKey={process.env.NEXT_PUBLIC_GOOGLE_MAPS_API_KEY}>
      <GoogleMap mapContainerStyle={containerStyle} centre={centre} zoom={10}>
        {locations.map((location, index) => (
          <Marker key={index} position={location} />
        ))}
      </GoogleMap>
    </LoadScript>
  )
}

export default MultipleMarkersMap
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

## Conclusion

This article has shown you how to integrate the Google Maps API into a Next.js application, from initial setup to implementing advanced features such as routes, calculating distances, and multiple markers. You can create interactive and customised map applications that enhance the user experience by following these steps.
