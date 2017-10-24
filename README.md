# Advanced Android App Development [13-10-2017]

## Stage 1 [13-10-2017]

## Stage 2 [14-10-2017]
**Fragments**  
*Fragments are Android app components that represent a self-contained portion of user interface in an activity. You can think of them as mini-activities. They are essentially reusable pieces of UI, similar to a layout similat to a layout or ViewGroup*

>It's important to note that a Fragment must always be embedded in an activity and the fragment's lifecycle is directly affected by the host activity's lifecycle. For example, when the activity is paused, so are all fragments in it, and when the activity is destroyed, so are all fragments.

*Fragments are reusable, modular (because they have their own lifecycle), and can be dynamically changed at runtime!*

**onCreateView()**  
*onCreateView() is where a fragment inflates its UI, hooksup any data source it needs, and then returns the created view to the host activity.*  

**onDestroyView()**  
And there's a corresponding on destroy view callback that can be called before a host activity is destroyed.*  

>Yes! When the host activity is created, both it, and the fragments it contains, call their onCreate methods. Then, right after this creation, fragments call their onCreateView method to inflate their view dynamically!

*Any class who want to be a fragment, "from chomu to fragment hahaha okay that enough go back to study pussy cat" must extends from Fragment and it's up to you use support.v4 Fragment or app.Fragment but this extension is important, because it's how Android knows to treat this class, and its lifecycle events and creation, as a fragment. Now every fragment will implement a couple of methods. The first is an empty constructor that's necessary for instantiating the fragment. The second is a method onCreateView, which is called when the fragment that we just created is inflates for display, similar to onCreate for an activity. So, make sure to implement for any fragment you create.*

>Every fragment needs to to be embedded in a host activity. 

**FragmentManager**  
*FragmentManager let's you add, remove, or replace fragments in an activity at runtime!*  
*FragmentManager facilitates these transactions:*
1. ADD
2. REMOVE
3. REPLACE


>Transactions let you create a dynamic user experience and help efficiently add and remove fragments wihtout you having to worry about the finer details of memory management. 

>To dynamically change fragments, you'll need a container view to reference their location and hold each fragment. This is often a empty FrameLayout 

**Containers are needed to use transactions:**  
1. ADD
2. REMOVE
3. REPLACE

>Static framents (that don't change during runtime) don not need a container

*Static fragments don't need transactions*  

*Make each fragment self-contained* -> *This just means that a single fragment will also contain code that define its layout and behavior, when it comes to user interaction. And it also means that generally, fragments can never directly communicate with one another. But then, how can you communicate between two self-contained fragments? Well all fragment to fragment communication can be done through a shared activity. To give a fragment the ability to communicate up to its host activity, it's good prectice to define an interface in the fragment class, and implement it within the activity. *

**Why interfaces?**  
*To keep fragments modular and reusable, you cannot have them communicate directly with one another or directly tied to a host activity. An interface gives you a way to communicate but also stay modular because it can be implemented by any host activity -- this way the fragment is not tied directly to an activity.*












