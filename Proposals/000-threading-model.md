# New threading model

#### The current threading model

- Does initial heavy duty setup on background thread
- The main thread takes over after initial setup
- Small incremental changes are done from main thread

```
~  Main   Background    Background
    |        |        
    |<-------| (setup)      
    |                 
    |--\              
    |<-/ (update constraints)             
    |                 
    |                      |
    |<---------------------| (update with new data)
    |
    |                
    |--\              
    |<-/ (update constraints)
    |        
    |--\              
    |<-/ (update constraints)
```

#### Problems with old model

- Updates with new data happens on a background thread as well which might interfere with main thread
- View tree and node tree is too tightly coupled
- Hard to write a bridge between solvers – we don't know which thread mutate solvers with new constraints

#### New proposal

- Users of the library is able to specify a worker queue up front which may be used for 1 or more node trees
- Updates from main has to be marshaled to worker
- Main never gets hold of the ALENode's
- Main receives and sends all updates with simple immutable summaries/structs/primitives

```
~  Main    Worker
    |        |
    |<-------|   
    |        |
    |------->§   
    |< - - - §  (async callback)
    |        |   
```

#### Reflection

Using ALE and its c++ api directly might cause confusion. Especially if you are considering this very common scenario (replace "view" with "node" in your head):

 - You have created a view hierarchy
 - You have another view hieararchy
 - You want to add the latter to the former

For this scenario it is important that both nodes share the same worker queue. The program should crash if they are using different worker queues.
