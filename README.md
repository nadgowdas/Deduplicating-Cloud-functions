** **

## Deduplicating-Cloud-functions Project Proposal

The purpose of this project is to design and implement a novel storage de-duplication framework for serverless platform in order to improve overall throughput of the platform.
** **

## 1.   Vision and Goals Of The Project:

The final product of this project will be a de-duplication service that leverages application-aware semantic-equivalence to identify duplicate data at storage system and avoids redundant invocation of functions on servers. Main goals include:
* Define and implement specialized data curation techniques 
* Optimize de-duplication data structure and indexing
* Perform data and event de-duplication to avoid redundant execution of stateless functions

## 2. Users/Personas Of The Project:

This section describes the principal user roles of the project together with the key characteristics of these roles. This information will inform the design and the user scenarios. A complete set of roles helps in ensuring that high-level requirements can be identified in the product backlog.

This framework will be used by researchers from BU, MIT, NEU, Harvard ,UMass and the paying users of MOC(economic save).

  **It does not target:**
  
    MOC admin users, who will work against the command line.
    Administrators of cloud services, who will continue to use the services of serverless functions.

  **It targets :**
  
    The openwhisk platform on MOC
    End users who just submits the stateless functions for executions without worrying internal details as it saves them money by saving     the functions calls in an instance.

** **

## 3.   Scope and Features Of The Project:

**What will be delivered?**

* Presents a faster framework for cloud providers: 

  * For providers who mostly deal with data generated from external end-points like IoT devices, cloud systems monitors, weather sensors, social media, mobile devices, etc

  * By avoiding container startup latency: Since most platforms execute stateless functions inside containers, eliminating redundant activation of functions results in low latency.

*  Presents a framework for increasing “performance/cost” for end-users: 

    * End-users will use this framework indirectly which will, in turn, decrease the application cost for them since this framework increases throughput.

    * Availability to increase throughput more by offering user to define PoVs: PoVs(Point of Variability) are parts of the data that is not important for the execution and should be ignored such as metadata. Availability of letting user choose those points allows a more fine-grained de-duplication.

* Scalability: This novel storage de-duplication framework is designed and will be implemented for serverless execution model which in principle is flexible regarding scaling. An application can be scaled automatically or by adjusting its capacity through toggling the units of consumption.

* Security: Security can be ensured by writing secure application code and tight access control over source code. 

**What will not be delivered?**

* This framework does not help save storage space since for every new data coming original data is stored multiple times.

* This system can only be implemented on storage closed-loop functions, which takes data from data storage and writes the result again to the data storage. However, external stimuli functions are not the part of this de-duplication design because they take their data from storage but then trigger external events.

** **

## 4. Solution Concept

This section provides a high-level outline of the solution.


Global Architectural Structure Of the Project:

This section provides a high-level architecture or a conceptual diagram showing the scope of the solution. If wireframes or visuals have already been done, this section could also be used to show how the intended solution will look. This section also provides a walkthrough explanation of the architectural structure. 

Design Implications and Discussion:

The picture shows the overall architecture for Sanity System. 
![alt text](https://github.com/bu-528-sp19/Deduplicating-Cloud-functions/blob/master/arch.PNG)
* **Data Storage** has the actual data from the multiple live running containers without any annotations or filtering.
* **Data Curation** filters each data event using either POV/filter based duplication. Then, it checks the checksum for each incoming data.
* **Sanity Controller** indexes each event into the hashmap which identifies if the event is duplicate for a function. If the event is duplicate, it gets the output reference for the result from the earlier invocation.
* **Function Rule Map** stores the rules to associate data events with respective functions.
* **Function dupMap** maintains checksum of all unique input data processed by each function 

## 5. Acceptance criteria

Minimum acceptance criteria is to prevent data duplication which in turn would prevent event duplication. 

The stretch goals are:

Scale this to a distributed platform

## 6.  Release Planning:

(Temporary plan)

Sprint 1: 

Familiarizing ourselves with the existing OpenWhisk architecture and how it will be integrated with MOC.

Getting insights into the existing prototype developed by the mentor.

