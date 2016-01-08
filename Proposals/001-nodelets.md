# Nodelets


### The current model

Nodes relations to views:

- creates them directly
- owns them directly
- manipulates them directly

#### Benefits

- easy to create new nodes
- easy to use instead of UIKit due to its imperative model


### New proposal

Nodes does not know about views at all. Through a "producer" the given node hierarchy can generate a nodelets hierarchy. The nodelets are immutable, lightweight, structs/classes with information about what's to be rendered and all layout props.

The nodelets can safely be created on a worker thread for then to be passed to main. A view hierarchy can be built or updated in react-style from the nodelets, updating/creating only what's necessary.

Nodes will then only be responsible for:

- layout/geometry
- optional: calculating intrinsic height and width
- optional: rendering

#### Benefits

- threading is easier
- focused code
- presenting errors can be done in a much cleaner manner with nodelets instead of manipulating views directly from nodes

#### Unanswered questions

- What about views which are updating cassowary variables like contentOffset, intrinsicHeight or similar?
- How rich should a nodelet be? Should it store frame, type, alpha, backgroundColor, node specific attributes etc?

#### Reflection

This is more similar to how AsyncDisplayKit, Redux and React works.

#### API example


```objective-c

@interface ALENodeLet : NSObject
@property (nonatomic, assign, readonly) CGRect frame;
@property (nonatomic, assign, readonly) CGFloat alpha;
@end

[factory nodeNamed:@"text" setupNode:^(ALENode *node) {

}];

```

```objective-c

@interface ALENodeLet : NSObject
@property (nonatomic, assign, readonly) CGRect frame;
@property (nonatomic, assign, readonly) CGFloat alpha;
@end

[factory nodeNamed:@"text" setupNode:^(ALETextNode *node, ALENodeSpec *spec, NSDictionary *doc) {
    node.text = [spec textWithDocument:doc];
} createNodelet:^ALENodeLet *(ALETextNode *node) {
    ALETextNodeLet *nodelet = [ALETextNodeLet initWithNode:node]; // reads geometry
    nodelet.content = node.content; // UIImage of rendered text
    return nodelet;
} applyNodelet:];
```
