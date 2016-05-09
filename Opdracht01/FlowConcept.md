## Proof-of-concept Flow ##

De gebruiker logt in via de front-end webapplicatie op de gitrepository waar hij een project kan uploaden.

Dit kan een Java, .NET, PHP, ... project zijn. Jenkins luistert (via poort 8080) naar de github repository voor changes in een repository.

De Jenkins server waar de applicatie gebuild wordt detecteerd een project op de repository en haalt deze binnen met een pull request.

Jenkins build de applicatie en voert een post-build process uit. Dit houdt in dat Jenkins de gebuilde applicatie upload naar een server..

De applicatie is meteen bereikbaar op de server.


