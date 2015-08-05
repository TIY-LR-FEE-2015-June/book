# Wednesday July 30, 2015

## Handlebars Precompiler

## Backbone.Events and Delegation of Responsibility

Yesterday we looked at a Character object:

    function Character(health, strength) {
        this.takeDamage = function(amount) {
            health = health - amount;
        };

        this.getStrength = function() {
            return strength;
        };
    }

And we discussed that an attack function like this would be a bit hard to know what object was modified, and gave us a bit too much control over our enemy:

    Character.prototype.attack = function(enemy) {
        enemy.takeDamage(this.getStrength());
    };

We flipped this function on it's head and rewrote it as `attackedBy`.
This properly managed what object is being modified and made sure that our current Character wasn't directly modifying it's `enemy`, but it made it a bit awkward because now we can't `attack` and start a confrontation.

Instead we can look at delegating reponsibility to other objects.
One tool for this is to use an event system.
Event systems allow you to TELL objects about something that has happened and then that object can be listened to in order to tell when that event has been triggered.

It may seem like semantics, but leaning on events to delegate tasks in your application can be incredibly powerful!
