# Car model 

---

To add a car model in CARLA, you need the model itself and a suitable physics model. Note that the physics model should be very very simple, so that the calculations are not so difficult/expensive.

The car model should also not be unnecessarily complicated, as this is only necessary for the optics, i.e. not every switch or cable flow needs to be modeled now.

If you need to "clean up" a model, i.e. make it less complicated, you can also do this with Blender (Merge Objects in Blender, Key: j). Keep in mind that the wheels must still be single objects, so they can't be joined, but the rest of the car can be an object.

So the following must be present: A model where the single wheels are still objects and the rest of the car is an object, i.e. you have a model which consists of five objects.

![[docs/source/images/blenderObjectHierarchy.png]]
