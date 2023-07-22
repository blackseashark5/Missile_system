# Missile_system
#include <stdio.h>
#include <math.h>

struct Position {
    double x;
    double y;
};

struct Velocity {
    double vx;
    double vy;
};

struct Missile {
    struct Position position;
    struct Velocity velocity;
};

double calculateDistance(struct Position p1, struct Position p2) {
    double dx = p2.x - p1.x;
    double dy = p2.y - p1.y;
    return sqrt(dx * dx + dy * dy);
}

void updateVelocity(struct Missile* missile, struct Position target, double acceleration) {
    double dx = target.x - missile->position.x;
    double dy = target.y - missile->position.y;
    double distance = calculateDistance(missile->position, target);
    
    missile->velocity.vx += (acceleration * dx) / distance;
    missile->velocity.vy += (acceleration * dy) / distance;
}

void updatePosition(struct Missile* missile, double timeStep) {
    missile->position.x += missile->velocity.vx * timeStep;
    missile->position.y += missile->velocity.vy * timeStep;
}

int main() {
    struct Missile missile;
    missile.position.x = 0.0;
    missile.position.y = 0.0;
    missile.velocity.vx = 0.0;
    missile.velocity.vy = 0.0;
    
    struct Position target;
    target.x = 100.0;
    target.y = 200.0;
    
    double acceleration = 10.0;
    double timeStep = 0.1;
    
    int iterations = 0;
    double distance = calculateDistance(missile.position, target);
    
    while (distance > 1.0) {
        updateVelocity(&missile, target, acceleration);
        updatePosition(&missile, timeStep);
        
        distance = calculateDistance(missile.position, target);
        
        printf("Iteration: %d, Distance: %f, Position: (%f, %f)\n", 
               iterations, distance, missile.position.x, missile.position.y);
        
        iterations++;
    }
    
    printf("Target reached in %d iterations!\n", iterations);
    
    return 0;
}


C++


#include <iostream>
#include <cmath>

struct Position {
    double x;
    double y;
};

struct Velocity {
    double vx;
    double vy;
};

struct Missile {
    Position position;
    Velocity velocity;
};

double calculateDistance(Position p1, Position p2) {
    double dx = p2.x - p1.x;
    double dy = p2.y - p1.y;
    return std::sqrt(dx * dx + dy * dy);
}

void updateVelocity(Missile& missile, Position target, double acceleration) {
    double dx = target.x - missile.position.x;
    double dy = target.y - missile.position.y;
    double distance = calculateDistance(missile.position, target);
    
    missile.velocity.vx += (acceleration * dx) / distance;
    missile.velocity.vy += (acceleration * dy) / distance;
}

void updatePosition(Missile& missile, double timeStep) {
    missile.position.x += missile.velocity.vx * timeStep;
    missile.position.y += missile.velocity.vy * timeStep;
}

int main() {
    Missile missile;
    missile.position.x = 0.0;
    missile.position.y = 0.0;
    missile.velocity.vx = 0.0;
    missile.velocity.vy = 0.0;
    
    Position target;
    target.x = 100.0;
    target.y = 200.0;
    
    double acceleration = 10.0;
    double timeStep = 0.1;
    
    int iterations = 0;
    double distance = calculateDistance(missile.position, target);
    
    while (distance > 1.0) {
        updateVelocity(missile, target, acceleration);
        updatePosition(missile, timeStep);
        
        distance = calculateDistance(missile.position, target);
        
        std::cout << "Iteration: " << iterations << ", Distance: " << distance << ", Position: ("
                  << missile.position.x << ", " << missile.position.y << ")\n";
        
        iterations++;
    }
    
    std::cout << "Target reached in " << iterations << " iterations!\n";
    
    return 0;
}
