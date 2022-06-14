lets make a traffic light system that doesn't suck.

	why is anyone waiting at a red light when no one else is around?
	if we had an 'expert' human managing traffic, we all agree there would be less traffic (can use his brain to control traffic optimally and cause the least amount of time wasted unnecessarily 

	lets implement a 'smart intersection' that gathers data about the people approaching/waiting at the crossing, and attempts to minimize the amount of time we sit at red lights.

	traffic isn't predictable, so light cycles shouldn't be either.  they should adapt to their surroundings.


TERMS:
A - Anger score
Entity - any 'person' we can about tracking (Car, Bike, Pedestrian)


SYSTEM REQUIREMENTS:
	we will need monitoring systems for the intersection
		- Cameras?
		- LIDAR?
		- Weight?

	some CPU where:
		f(Data) -> [weights for how much each light cluster (lights that can be on at the same time) 'wants' to be on]

	Data will need to include:
		A cost for swapping the lights, system will try to not swap the lights more than some frequency X swaps/minute
		time each entity has been waiting at the intersection.
			system wants to reduce an Anger (A) metric for each entity, which grows with time spent waiting.
			smaller effects to A will include:
				speed approaching intersection.  Imagine a scenario where one direction of traffic has just cleared out, but one last car is coming towards the intersection from that same direction of traffic.  the system should be smart enough to wait just long enough to allow the last car through, before swapping the green light to the waiting traffic (assuming the costs of them waiting are still less) so that the fast approaching car will not have to reduce it's speed rapidly
			Anger (A) should scale as a X^n type function w.r.t. time.  1 second is more painful for someone who has been waiting 100 seconds, then it is for someone who has only been waiting 10 seconds.



SYSTEM STRUCTURE

class 'Person' for each waiting entity
	has attributes: velocity, time_waited, Anger


simulate an intersection for testing purposes
	can later be used to translate the Visual data into some workable environment/form

ques to represent Entities waiting for their turn to pass through at each lane (car lane, bike lane, pedestrian lane)
	pop off entities when they've passed through
	some way to remove entities if they do unexpected shit (illegal U-turns, etc.)
	
AI for entity detection and tracking?
	want a way to track entities around the intersection and how they persist throughout time


We should cluster bikes, cars, and pedestrians by groups that can go together.  Each intersection should be setup by groups (1...n) where n is the minimum number of possible pairings that cannot simultaniously go through the intersection.


