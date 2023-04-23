# Data Definitions

Here the data definitions to be used in the smart contracts:

Agreements:  
{. 
    id:uint32. 
    owners:[address,address..],  
    ipfs: address,  
    escrow: uint256,  
    epochend: uint256,  
    status: integer,                         
}. 

The Status can have the following values: 
- 0=draft,  
- 1=partially signed. 
- 2=fully signed. 
- 3= Arbitration. 
- 9= Completed. 

Users: {  
    address: address,  
    country: bytes,  
    eccpublickey: bytesarray,  
    kyberpublickey: bytesarray,  
}  
country is the country code of the user to apply the governing law in case that all the parties are in the same country. 

Settings:
{
    ContractOwner: address,
    NewAccountFees: uint256,
    SubmissionFees: uint256,
    TemplateFees: uint256,
    TemplateFeesContributor: uint256,
    ArbitrationFees: uint256,
    ArbitrationFeesArbitrator: uint256,
    MinArbitrationFeesArbitrator: uint256,
    Decimals: integer,
    ActiveInactive: bool,
    lastagreementid: uint32,
    lastarbitrationid: uint32,
    MaxAmountSingleArbitrator:uint256,
}
Contract Owner is the one that is enabled to change the settings
Arbitration fees are a percentage of the value of the contract
MinArbitrationFeesArbitrator is the minimum amount for the arbitrator.
ActiveInactive allows to suspend/reactivate the smart contracts (emergency lockdown).


TemplatesAgreement:
{
    contributor: address,
    ipfs: ipfsaddress,
}

Contributors:
{
    contributor: address,
    stakesbalance: uint256,
    rewardsbalance: uint256
}

Escrow:{
    agreementid: uint32,
    depositor: address,
    recipient: address
    amount: uint256,
    balance: uint256,
    status: integer,
    epochexpiry: uint256,
}

status values can be:
- 0 = Waiting for deposit
- 1 = Deposit Received
- 2 = Arbitration
- 3 = Returned
- 9 = Released

epochexpiry, is the date/time in seconds of expiry of the escrow.
If there are no arbitration open, the recipient can claim it.

Arbitration: {
    id:uint32
    agreementid: uint32,
    arbitrators:[address,address,..]
    votes[address,address,...],
    votetransfer: [{arbitrator,address,amount},{..}]
    decision: [{address,amount},{..}]
    balancefees: uint256,
    epochexpiry: uint64
}
epochexpiry is the last date/time for the parties to submit their supporting documents.
votetransfer are the votes of the arbitrators
decision is the result of the votes above making an average in case of difformity in the amounts but in the same direction. if the direction is opposite the majority win.

ArbitrationClaims: {
    arbitrationid: uint32,
    counterpart: address,
    refundclaim: uint256,
    ipfsdocs:[address,address,address]
}

Arbitrators: {
    arbitrator: address,
    language: bytes,
    country: bytes,
    stakesbalance: uint256,
    rewardsbalance: uint256,
    alignedvotes: uint,
    disalignedvotes: uint,
}
language code the arbitrator can work for.
country code the arbitrator can work for when all the parties are in the same country.




