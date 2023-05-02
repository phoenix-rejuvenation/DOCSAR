# DOCSAR: The Distributed Database of Chemical Substances and Reactions

DOCSAR is a blockchain-based platform designed to democratize access to chemical knowledge. It allows users to store and share comprehensive data on chemical substances and reactions, facilitating machine learning models and accelerating research in medicine, biotechnology, and material design.

Note: Links for the motivation behind this project: https://pubs.acs.org/doi/10.1021/acs.jcim.1c01140

## System Components

1. **User Management**: Every user in the system is represented as a unique ID, a pair of keys (public and private), a contact address, a contact protocol, and a set of grants that define their permissions. The contact protocol and address are flexible, future-proofing the platform against changes in communication technology.

2. **Points System**: The system incentivizes user contributions via a points system. Actions performed by users, such as adding substance and reaction definitions, and verifying existing definitions, are associated with points. These points can be transferred between users in transaction blocks. The points associated with each action are defined globally by the supreme account in a Points Definition Block.

3. **Chemical Substance and Reaction Definitions**: Users can add blocks to the blockchain containing detailed definitions of chemical substances and reactions. These definitions are not limited to basic information such as IUPAC names, molecular formulas, molecular weights, but can also include extensive data on structural information, properties, reaction conditions, reaction mechanisms, and more.

## Block Schemas

Several types of blocks can be added to the DOCSAR blockchain:

1. **User Block**: Contains user ID, public key, contact information (protocol and address), and grant level. The block schema is as follows:
```json
{
  "UserID": "string",
  "PublicKey": "string",
  "Contact": {
    "Protocol": "string",
    "Address": "string"
  },
  "Grant": "string"
}
```
2. **Points Definition Block**: Issued by the supreme account, it defines the number of points associated with each action type.
```json
{
  "BlockIssuerID": "string",
  "ActionTypePoints": [
    {
      "ActionType": "string",
      "Points": "float"
    }
  ]
}
```
3. **Transaction Block**: Records the transfer of points between users.
```json
{
  "SenderUserID": "string",
  "ReceiverUserID": "string",
  "Points": "float",
  "Timestamp": "string"
}
```
4. **Chemical Substance Definition Block**: Contains information about a chemical substance.
```json
{
  "BlockIssuerID": "string",
  "SubstanceID": "string",
  "SubstanceData": {
    "IUPACName": "string",
    "MolecularFormula": "string",
    "MolecularWeight": "float",
    "Structure": "string",
    "Properties": {
      "Physical": "string",
      "Chemical": "string"
    },
    "SafetyNote": "string",
    "ToxicityIndex": "number"
  }
}
```
5. **Chemical Reaction Definition Block**: Contains information about a chemical reaction.
```json
{
  "BlockIssuerID": "string",
  "ReactionID": "string",
  "ReactionData": {
    "Reactants": [
      {
        "SubstanceID": "string",
        "Quantity": "float"
      }
    ],
    "Products": [
      {
        "SubstanceID": "string",
        "Quantity": "float"
      }
    ],
    "Conditions": "string",
    "Mechanism": "string"
  }
}
```
5. **Chemical Reaction/Substance Verification Block**: Created once per cemical substance or reaction.
```json
{
  "BlockIssuerID": "string",
  "NowVerifiedBlockID" : "string"
}
```
## Grant Levels

DOCSAR uses a system of grant levels to control user permissions:

1. **Alpha**: The highest level of privilege. There is only one alpha account, and
it can perform all actions, including defining the points associated with each action type.

2. **Grant A**: Users with Grant A can:

    - Add blocks that attribute new grants to other users.
    - Downgrade the grant of another user, provided it's not Grant A.
    - Add and verify chemical substance and reaction definition blocks.
    - Erase or update definitions of chemical substances or reactions by adding an update block, even if they are verified.
    - Declare that another block is verified, provided the block contains a definition of a chemical substance or reaction. A hash of a document containing experiment results or an essay should be provided.

3. **Grant B**: Users with Grant B can:

    - Add blocks that attribute Grant C to other users.
    - Add and verify chemical substance and reaction definition blocks.
    - They cannot erase or update the definition of a chemical substance or reaction by adding an update block.

4. **Grant C**: Users with Grant C can:

    - Add chemical substance and reaction definition blocks but cannot verify them.
    - They cannot erase or update the definition of a chemical substance or reaction by adding an update block.

## Future Directions

DOCSAR is designed to be a future-proof, self-contained system. The flexible user contact system allows for changes in communication technology. The comprehensive chemical data schemas and flexible definitions permit the inclusion of diverse and detailed chemical information, with potential applications in numerous fields of research and industry. By democratizing access to chemical data and incentivizing contributions, DOCSAR aims to accelerate the advance of chemical knowledge.
