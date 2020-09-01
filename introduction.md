> A distributed system is one in which the failure of a computer you didn't even know existed can render your own computer unusable.
> - Leslie Lamport

# Introduction

- [Prerequisites](#prerequisites)
- [Project](#byop-build-your-own-project)
  - [Requirements](#project-requirements)
  - [Ideas](#project-ideas)
- [Milestones](#milestones)

The purpose of these labs is to study characteristics of distributed systems and apply them in practice.
Distributed Systems labs are intended to be a single project, split into several milestones. Each milestone is focused on a specific objective and a set of distributed system characteristics.

## Prerequisites

There are several prerequisites that aren't covered in this course:
- Concurrency primitives and thread-safe collections;
- Network programming:
    - OSI Model;
    - Network and Transport protocols;
- Data representation and serialization/deserialization;
- Basic understanding of communication protocols and APIs;

## BYOP (Build Your Own Project)

The very first step is to define project requirements you're going to work on.
The end-goal is to build a distributed system, your project must be complex enough to be implemented as a distributed system.
Thus there are several requirements your project must meet.

### Project requirements

- the project must contain several components that can run on different computers and communicate with each other via network;
- some components exchange messages via a messaging agent / broker;
- one or more components must expose public HTTP-based API;

**There are no programming language constraints.**
However, it's strongly recommended to choose a language that has sane networking and concurrency primitives.

**Note:** The project can be executed in teams of up to 3 people.

### Project ideas

There's a huge number of real-world problems that can be solved with a distributed system.
Feel free to borrow any of the ideas described below or come up with your own.

#### Smart-house

A smart-house system has very limited use if it consists of only a bunch of sensors.
Build the core of a smart-house system (sensors and toggles can be replaced with some stubs):
- data store that collects timeseries data and allows querying it (for some charts perhaps);
- "bridge" components that collect data from sensors and forwards to the data store. It can also receive commands and dispatch it to a toggle/device;
- a "control plane" component that exposes API for devices management;

#### Expense manager

#### An airline reservation system

#### Warehouse accounting system

## Milestones

Each milestone is focused on some specific objectives and only a part of your project.
Deadline for submitting a milestone for grading is beginning of the next milestone.

### Message brokers

Identify what components of your project can communicate with each other using a message broker.
This allows decoupling decoupling communication between different components using a message broker.

Example: In the "Smart-house" project, "bridge" component and "control plane" component should exchange messages via a broker.

Go to [Message Brokers lab](lab1.md).

### Web proxy

### Cloud apps
