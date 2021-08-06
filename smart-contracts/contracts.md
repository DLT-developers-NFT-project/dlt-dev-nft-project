# Info on smart contract implementations
## CryptoKitties

| Contract             | Inherits                   | Usage                                                                                                                                                   |
|----------------------|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| Ownable              | -                          | The Ownable contract has an owner address, and provides basic authorization control functions, this simplifies the implementation of "user permissions" |
| ERC721               | -                          | Interface for contracts conforming to ERC-721: Non-Fungible Tokens                                                                                      |
| GeneScienceInterface | -                          | Generate genetic combinations to be passed down to the children                                                                                         |
| KittyAccessControl   | -                          | Controls access control for CryptoKitties                                                                                                               |
| KittyBase            | KittyAccessControl         | Base contract for CryptoKitties. Holds all common structs, events and base variables                                                                    |
| ERC721Metadata       | -                          | Responsible for generating metadata for the octopuses                                                                                                   |
| KittyOwnership       | -                          | Manages ownership                                                                                                                                       |
| KittyBreeding        | KittyOwnership             | A facet of KittyCore that manages Kitty siring, gestation, and birth                                                                                    |
| ClockAuctionBase     | -                          | Contains models, variables, and internal methods for the auction                                                                                        |
| Pausable             | Ownable                    | Base contract which allows children to implement an emergency stop mechanism                                                                            |
| ClockAuction         | Pausable, ClockAuctionBase | Clock auction for non-fungible tokens                                                                                                                   |
| SiringClockAuction   | ClockAuction               | Reverse auction modified for siring                                                                                                                     |
| SaleClockAuction     | ClockAuction               | Clock auction modified for sale of kitties                                                                                                              |
| KittyAuction         | KittyBreeding              | Handles creating auctions for sale and siring of kitties                                                                                                |
| KittyMinting         | KittyAuction               | Handles all functions related to creating kittens                                                                                                       |
| KittyCore            | KittyMinting               | Main CryptoKitties contract                                                                                                                             |

### Details

- Ownable contract

| Variable | Type    | Visibility |
|-----------|---------|------------|
| owner     | address | public     |

| Method            | Type     | Visibility | Parameters         | Returns | Usage |
|-------------------|----------|------------|--------------------|---------|-------|
| Ownable           | function | default    | -                  | -       |       |
| onlyOwner         | modifier | default    | -                  | -       |       |
| transferOwnership | function | default    | newOwner (address) | -       |       |


## CryptoZombies 

Note: We're going with this implementation

| Contract        | Inherits             | Usage                                                                                                                                                   |
|-----------------|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| Ownable         | -                    | The Ownable contract has an owner address, and provides basic authorization control functions, this simplifies the implementation of "user permissions" |
| ERC721          | -                    | Interface for contracts conforming to ERC-721: Non-Fungible Tokens                                                                                      |
| ZombieFactory   | Ownable              | Stores zombies in an array, creates new zombies, and assigns a unique and random apparenace for each zombie                                             |
| KittyInterface  | -                    | To interact with the CryptoKitties smart contract                                                                                                       |
| ZombieFeeding   | ZombieFactory        | Sets conditions for zombies to feed and multiply                                                                                                        |
| ZombieHelper    | ZombieFeeding        | Contains additional helper methods                                                                                                                      |
| ZombieAttack    | ZombieHelper         | Sets conditions for the zombie battles                                                                                                                  |
| ZombieOwnership | ZombieAttack, ERC721 | Stores all the ERC721 logic                                                                                                                             |


### Details

- Ownable contract

| Variable | Type    | Visibility |
|----------|---------|------------|
| owner    | address | private    |

| Method            | Type     | Visibility | Parameters         | Returns | Usage |
|-------------------|----------|------------|--------------------|---------|-------|
| owner             | function | public     | -                  | address |       |
| onlyOwner         | modifier | default    | -                  | -       |       |
| isOwner           | function | public     | -                  | bool    |       |
| renounceOwnership | function | public     | -                  | -       |       |
| transferOwnership | function | public     | newOwner (address) | -       |       |
| transferOwnership | function | internal   | newOwner (address) | -       |       |