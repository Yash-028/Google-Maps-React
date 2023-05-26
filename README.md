# Google-Maps-React

Please Refer to this link for more info - https://www.npmjs.com/package/@googlemaps/react-wrapper

# Description

Wrap React components with this library to load the Google Maps JavaScript API.

import { Wrapper } from "@googlemaps/react-wrapper";

const MyApp = () => (
<Wrapper apiKey={"YOUR_API_KEY"}>
<MyMapComponent />
</Wrapper>
);
The preceding example will not render any elements unless the Google Maps JavaScript API is successfully loaded. To handle error cases and the time until load is complete, it is recommended to provide render props.

import { Wrapper, Status } from "@googlemaps/react-wrapper";

const render = (status) => {
switch (status) {
case Status.LOADING:
return <Spinner />;
case Status.FAILURE:
return <ErrorComponent />;
case Status.SUCCESS:
return <MyMapComponent />;
}
};

const MyApp = () => <Wrapper apiKey={"YOUR_API_KEY"} render={render} />;
When combining children and render props, the children will render on success and the render prop will be executed for other status values.

import { Wrapper, Status } from "@googlemaps/react-wrapper";

const render = (status: Status): ReactElement => {
if (status === Status.FAILURE) return <ErrorComponent />;
return <Spinner />;
};

const MyApp = () => (
<Wrapper apiKey={"YOUR_API_KEY"} render={render}>
<MyMapComponent />
</Wrapper>
);
@googlemaps/js-api-loader
This wrapper uses @googlemaps/js-api-loader to load the Google Maps JavaScript API. This library uses a singleton pattern and will not attempt to load the library more than once. All options accepted by @googlemaps/js-api-loader are also accepted as props to the wrapper component.

# MyMapComponent

The following snippets demonstrates the usage of useRef and useEffect hooks with Google Maps.

function MyMapComponent({
center,
zoom,
}: {
center: google.maps.LatLngLiteral;
zoom: number;
}) {
const ref = useRef();

useEffect(() => {
new window.google.maps.Map(ref.current, {
center,
zoom,
});
});

return <div ref={ref} id="map" />;
}
Examples
See the examples folder for additional usage patterns.

Basic Demo
Install
Available via npm as the package @googlemaps/react-wrapper.

npm i @googlemaps/react-wrapper
or

yarn add @googlemaps/react-wrapper
For TypeScript support additionally install type definitions.

npm i -D @types/google.maps
or

yarn add -D @types/google.maps
Documentation
The reference documentation can be found at this link.

# Support

This library is community supported. We're comfortable enough with the stability and features of the library that we want you to build real production applications on it.

If you find a bug, or have a feature suggestion, please log an issue. If you'd like to contribute, please read How to Contribute.
