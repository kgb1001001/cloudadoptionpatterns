# Sidebar:  Why add Event Driven Architecture?

One of the more common questions we receive when discussing why you need to add Event Driven Architecture to an existing Services-Based architecture (for instance one based on REST) is "What does this do that we can't do with traditional REST service calls?"  It's easiest to understand the difference, and the advantages of an Event-Driven approach, through an example.  A good example that is easy to understand is the effect on a travel itinerary where a flight runs late.  What effects can a flight running late have?

*	If you have a connecting flight, you may miss it and need to be rebooked on a later flight
*	If you have a rental car reservation, you won’t need it until later
*	If you have a hotel reservation and you won’t get to that city until the next day, you won’t need the reservation for tonight
*	If you get stuck at a connecting airport overnight, you’ll need a hotel reservation in that city
*	If you have a meeting scheduled at your destination, you may need to delay the meeting time or cancel it, in which case you need to notify the other attendees
*	Your loved ones, colleagues, pet sitter, etc. may want a courtesy message letting them know you’ve been delayed

These are the consequences and adjustments per passenger or party traveling together. Multiply them times the 100 or so passengers on the flight. There are also consequences for the airlines:

*	The plane will be delayed for its next flight. Another aircraft may need to be assigned for the next flight and this aircraft reassigned.
*	The flight crew may miss their next flights. The flights must be delayed or replacement crews assigned.
*	The flight crew may exceed their work limits, meaning that other flights they work on must be delayed or new crews assigned.
*	Crew members who are passengers on the current flight may not be available for their assigned flights.
*	The flight’s destination gate can or should be changed. Likewise for the gate, baggage, cleaning, and food service crews scheduled to handle the flight when it arrives.

All these consequences occur because one flight is late.  Once the airline knows its flight is late, what can it do to mitigate these consequences?

## A Centralized Solution

The Airline could know about the full travel itinerary of each passenger of the flight: not only connecting flights on the same airline, but also flights on other airlines, reservations for rental cars and hotels, and any other travel arrangements. For privacy reasons, the passenger may not be comfortable revealing all of this information to the airline. The airline doesn’t want to be responsible for storing all of this information and for processing updates to frequently changing travel plans. And even if the airline had the most up-to-date itinerary, it doesn’t want to be responsible for having to change the reservations with all of these other travel service providers.
The scenario becomes even more complex for updating a passenger’s plans on arrival. What meetings is he scheduled for and who was he meeting with? Who is meeting him at the airport or shortly thereafter? What services, such as house sitting, need to continue until the passenger arrives at his destination? What people are affected and how can they be contacted?  However, the airline doesn’t want all of this responsibility. Likewise, the passengers don’t want to divulge all of this information.  Luckily, there is a better approach using Events.

## Event Notification Solution

The airlines already have a solution to this problem. On most airlines, you can register for notification of changes to a flight’s departure or arrival time. The notifications can be sent by text, voice, or email. This service can be used by passengers on a flight and by meeting passengers for a flight. This notification capability can be combined with programmatic dependency registration and notification messaging to modify plans when a flight is late. The plan modification is distributed to dependents, each adjusting its own part of the plan according to its own rules specific for it particular service.

Some examples of how airline flight notification can help a passenger manage the consequences:

* An itinerary object in the airline’s computer represents a passenger’s flights. It receives notification of the flight delay, determines whether the passenger will miss a connection, and schedules new flights accordingly.
* If the itinerary introduces an overnight stay in a connecting city, the airline reserves a hotel room in that city for the passenger.
* The reservation record in a rental car company’s computer registers for notifications for the renter’s incoming flight. When it receives notification of a delay, according to company business rules, it releases the renter’s car to other customers and reserves a different car that will be available at the flight’s new arrival time.
* The hotel’s computer has a similar reservation. When the airline itinerary announces the incoming flight has changed to the next day, the hotel cancels the passenger’s reservation for that night and makes the room available for other customers.
* The passenger’s travel agency or executive assistant has his full itinerary record. When it receives notification, it can handle verifying rescheduling by the individual services, resolve any discrepancies, and surface any issues to human representatives.
* The passenger’s calendar program (Notes, Outlook, etc.) can register dependency with the airline itinerary and/or travel agency itinerary. When the itinerary changes, the calendar (perhaps with human assistance) can look for conflicts, start rescheduling meetings, and notifying meeting participants.

The flight notifications can also help the airline manage its own resources:

*	The aircraft has an itinerary representing its flights. If a delay means it will miss a connection, the airline can employ business rules to delay the aircraft’s subsequent flights or find replacement aircraft.
*	The crew members (pilots, flight attendants, etc.) have itineraries, hours worked, and rules representing constraints on hours worked and schedules. Upon notification of a delay, it can delay the crew members’ subsequent flights or reschedule the crew members and find substitutes.
*	Crew members riding as passengers have subsequent work itineraries represented as meetings. When a flight is delayed, these meetings/itineraries must be rescheduled.
*	Ground crew members have meetings scheduled to service the aircraft, meetings that must be rescheduled when a delay occurs. Likewise, resources like gates and fuel trucks are scheduled for meetings that must be rescheduled.

This solution depends  on each service vendor being able to react to notifications and reschedule accordingly. But if that’s in place, all the airlines must do it:
*	Maintain a schedule for each flight
*	Maintain an itinerary for each passenger composed of flight schedules
*	Provide the means to register dependency on either of these objects (flight and/or itinerary)
*	Provide notification to an object’s dependents when the object changes 

In this way, event notification can be used to provide complex coordination amongst separate vendors working together to provide coordinated services. Each vendor does is responsible for adjusting its own part of the service. No vendor has more information than it needs except to know what resources it depends on (such as a rental car company or hotel needing to know a customer’s incoming flight).
