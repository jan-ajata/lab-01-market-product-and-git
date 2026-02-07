
## Product Choice

Yandex Go  
<https://taxi.yandex.ru/>  
Provides access to taxis.  

## Main components

![Yandex Go Component Diagram](../diagrams/out/yandex-go/architecture-component/Component%20Diagram.svg)
[Yandex Go Component Diagram puml code](../diagrams/src/yandex-go/architecture-component.puml)  
  
Maps & Routing Service: Connect to Yandex Maps in order to find closest taxis.  
Payment Service: Connects to Yandex Pay and provides a way to pay for services.  
Notification Serivce: Provides spam messages.  
Dispatch Service: Controls the dispatch of taxis to user location.  
API Gateway: Makes a uniform connection through this layer to users directly.  

## Data flow

![Yandex Go Flow diagram](../../docs/diagrams/out/yandex-go/architecture-sequence/Sequence%20Diagram.svg)  
[Yandex Go Flow diagram puml code](../../docs/diagrams/src/yandex-go/architecture-sequence.puml)

Booking & Async Dispatch: starts with order creating, initializes ride and validates the payment method. Assigns to the database that order is in SEARCHING status, find drivers through Geospatial Search. After finding the drivers it updates the status of the orded to ASSIGNED and creates an event of RideAssigned, which is then transformed into a push notification on users device. After that it updates the map with showing the driver.

## Deployment

![Yandex Go Deployment diagram](../../docs/diagrams/out/yandex-go/architecture-deployment/Deployment%20Diagram.svg)  
[Yandex Go Deployment diagram puml code](../../docs/diagrams/src/yandex-go/architecture-deployment.puml)  
The components are deployed mostly on Yandex Cloud.

## Assumptions

I assume that Notification Service primary function is spam messages.

## Open questions

What are the exact algorithms that go into dispatching approporiate drivers, is it purely based on distance and selected type or are there other factors?
