### Archtecture Layout
This doc aims to make the vision of reponsability to isolate the application logic itself and all its underling complexities from the out borders os IO stuff.

## layers of connections

### Out borders
- Http (in, out)
- Events (in, out)
- DBs and other IO components such as Redis our any other closer to the application domain, however still IO and still on the borders in a way.

#### The diplomacy and orchestrators
- Orchestrators
- Diplomats

#### Core business Logic
- As pure functions as possible, NO IO's no network no DBs no nothing of that.

## Quick samples
<p>http call for the app to get a list of a given resource</p> 
<p> eg. http in -> diplomat handle contract -> [orchestrator [-> logic]] response back</p>
<b> Looks over complicated for such simple example and it is.</b>

<p>But the motivation behind this is not to facilitate nor complicate simple resource serving APIs, but complex domain applications handling complex domains.</p>

<p>Example of a complex transaction responsible http endpoint POST</p>

<p>http in -> diplomat -> orchestrator 
[http out to another service to check a particupar resource state.<br>
db call to get own resource state,
handle word change logic]
-> logic(world, action) -> new world
-> orchestrator [handles state changes, notify other services via events]<br> -> response back </p>

<b>Looks too much still? Shall we talk about test of such complex business scenarios then?</b>

<p> In the abouve example, even with all the crazy side effects that happens due to this POST endpoint beeing called, the business logic is completely isolated and free of dependencies on a function of type (A) => B. It does not get any easier than that to test.</p>