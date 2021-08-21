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


- ZombieFactory contract

| Variable     | Type | Visibility |
|--------------|------|------------|
| dnaDigits    | uint | default    |
| dnaModulus   | uint | default    |
| cooldownTime | uint | default    |
| zombies | struct array | public    |

| Method             | Type     | Visibility | Parameters                  | Returns | Usage |
|--------------------|----------|------------|-----------------------------|---------|-------|
| zombieToOwner      | mapping  | public     | uint                        | address |       |
| ownerZombieCount   | mapping  | default    | address                     | uint    |       |
| _createZombie      | function | internal   | _name (string), _dna (uint) | -       |       |
| _generateRandomDna | function | private    | _str (string)               | uint    |       |
| createRandomZombie | function | public     | _name (string)              | -       |       |


- ZombieFeeding contract

| Variable | Type    | Visibility |
|----------|---------|------------|
| kittyContract   | KittyInterface | default    |

| Method             | Type     | Visibility | Parameters                  | Returns | Usage |
|--------------------|----------|------------|-----------------------------|---------|-------|
| ownerOf            | modifier | default    | _zombieId (uint)            | -       |       |
| setKittyContractAddress | function | external    | _address (address)    | -       |       |
| _triggerCooldown | function | internal    | _zombie (Zombie - struct)    | -       |       |
| _isReady | function | internal    | _zombie (Zombie - struct)    | bool      |       |
| feedAndMultiply | function | internal    | _zombieId (uint), _targetDna (uint), _species (string)  | bool      |       |
| feedOnKitty | function | public    | _zombieId (uint), _kittyId (uint) | bool      |       |


- ZombieHelper contract

| Variable | Type    | Visibility |
|----------|---------|------------|
| levelUpFee   | uint | default    |


| Method             | Type     | Visibility | Parameters                  | Returns | Usage |
|--------------------|----------|------------|-----------------------------|---------|-------|
| aboveLevel            | modifier | default |  _level (uint), _zombieId (uint)  | -  |       |
| withdraw | function | external | - | - |
| setLevelUpFee | function | external | _fee (uint) | - |  |
| levelUp | function, payable | external | _zombieId (uint) | - |  |
| changeName | function | external | _zombieId (uint), _newName (string) | - |  |
| changeDna | function | external | _zombieId (uint), _newDna (string) | - |  |
| getZombiesByOwner | function | external | _owner (address) | uint[] |  |


- ZombieAttack contract

| Variable | Type    | Visibility |
|----------|---------|------------|
| randNonce   | uint | default    |
| attackVictoryProbability | uint | default    |

| Method             | Type     | Visibility | Parameters                  | Returns | Usage |
|--------------------|----------|------------|-----------------------------|---------|-------|
| randMod            | function | internal   |  _modulus (uint)            | uint |       |
| attack             | function | external   |  _zombieId (uint), _targetId (uint) | - |       |


- ZombieOwnership contract

| Method             | Type     | Visibility | Parameters                  | Returns | Usage |
|--------------------|----------|------------|-----------------------------|---------|-------|
| zombieApprovals    | mapping | default   |  uint            | address |       |
| balanceOf          | function | external   |  _owner (address) | ownerZombieCount (uint256) |       |
| ownerOf          | function | external   |  _tokenId (uint256) | zombieToOwner (address) |       |
| _transfer        | function | private   |  _from (address),  _to (address),  _tokenId (uint256) | - |       |
| transferFrom      | function, payable | external   |  _from (address),  _to (address),  _tokenId (uint256) | - |       |
| approve      | function, payable | external   |  _approved (address),  _tokenId (uint256) | - |       |
