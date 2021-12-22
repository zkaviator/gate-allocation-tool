# gate-allocation-tool
A tool for assigning gates at airports throughout New Zealand airspace

This tool serves as a helper to air traffic controllers on the VATSIM Network operating in VATSIM New Zealand Airspace to assign gates to aircraft once aircraft arrive in their respective arrival airports inside VATNZ airspace. 

This tool takes in a aircraft that is connected to the VATSIM Network flying within or into VATNZ airspace, The tool calls to the VATSIM API to verify if the aircraft exists on the VATSIM Network and once verified, retrieves its origin and destination airports. The tool with this information, if the destination airport is within VATNZ airspace, makes a choice on gates at the destination airport to be assigned to the aircraft. 

The tool as a first choice, calls the aviationstack API to retrieve real world data involving that flight. If the real world flight is operating on the same day as the VATSIM flight with the same callsign, flying the same route and has a stand allocation, the tool then checks again if the stand the real world flight is taking can be taken by the VATSIM flight (if the aircraft on VATSIM can park at that stand firstly, and secondly if that stand is not occupied by another aircraft). If all these checks pass, then the tool assigns the VATSIM flight the same stand as the real world flight. 

If one of these checks fail (no real world flight matching the callsign exists, a real world callsign exists but not on the same route, no stand allocation exists for the real world flight, the stand the real world flight is parking at can't be occupied by the VATSIM flight (VATSIM aircraft too big compared to real flight) or the real world stand allocation is occupied by another VATSIM user), then a random allocation of a stand will take place given a database of gates depending on whether the flight is international or domestic, what aircraft type is being operated, whether the flight is passenger or cargo, and what airline the aircraft is operating for. The tool will also distinguish between scheduled commercial passenger or cargo flights, general aviation flights, business jet flights, and military operations. 

The random allocation chooses a random gate based on the criteria listed and does the final two checks again, whether the aircraft is too big to fit in that stand or whether the stand is occupied. If these two checks pass, the gate is assigned. 

If no possible stands can be assigned out of a pool, then the tool will return no gate allocation and the controller can by their discretion pick a stand or offer the pilot a choice of what stand to park at.
