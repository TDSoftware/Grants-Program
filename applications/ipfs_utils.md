# W3F Grant Proposal

- **Project Name:** substrate IPFS utilities
- **Team Name:** [TDSoftware](https://www.tdsoftware.de/)
- **Payment Address:**
- **Level:** 



## Project Overview

This application is about the utilities of Substrate within IPFS.


### Overview

IPFS is a web3 solution to handle big-size data or not structure data, and there is no good integration between substrate and IPFS.

Currently, the easy way to record IPFS CID on a substrate-based blockchain is to call extrinsic and pass the IPFS CID as an input parameter, and then the IPFS CID is stored on a chain.  And the CID is normally related to some non-fungible token(NFT), and becomes one metadata of the token.

In the solution, it will need much more affairs to validation process on the chain side, if the developer wants to make sure and trust the input CID will point to the corresponding file on the chain.  Besides, the CID is listed via gRPC as a string field, it can not be presented event the browser already supports IPFS.


### Project Details

#### Upload utilities
In the first part, detailed research is needed to upload data to IPFS, including
- Accepting bytes as an input parameter of extrinsic
- Uploading `&[u8]` or `[u8]` to IPFS, may or may not in off-chain worker
- Storing CID information on chain, also the CID version 0 and CID version 1 could be handled
- Benchmarking on the extrinsic call to know the maximum size of bytes can work 

#### Read/access utilities
In the second part, the redirect feature will be provided based on the gRPC mechanism, the details are listed
- Accept a function with `Result<String>` return, and take the content of String as the location to redirect
- Developer can define the redirect location as CIDv0 or CIDV1.
- Base on Post/Redirect/Get ([PRG](https://en.wikipedia.org/wiki/Post/Redirect/Get)) pattern
- The return code is HTTP 303 See Other
- User can `#[prg(name = "nft_getArtworkById")]`


### Ecosystem Fit

The implementation helps people using IPFS with substrate, this is a common scenario.
People fork substrate and try to solve this in [offchain_ipfs](https://github.com/rs-ipfs/substrate/tree/offchain_ipfs),
but it is based on substrate about two years before, and not actively updated.
It is good to make IPFS utilities with grant.


#### Technology Stack 

Blockchain
- Substrate
- Rust
- IPFS

## Team :busts_in_silhouette:

### Team members

- Sascha Dobschal

The team setup might change depending on the availability at TDSoftware. With 40+ employees, TDSoftware has various developers that might contribute to the project. In all probability the members listed above will attend.

### Contact

- **Contact Name:** Sascha Dobschal
- **Contact Email:** s.dobschal@tdsoftware.de


### Legal Structure

- **Registered Address:** Schlossgasse 20, 07743 Jena, Germany
- **Registered Legal Entity:** TDSoftware GmbH


### Team's experience
We have years of experience bringing ideas to life with a user-centered focus using blockchain and mobile technology. We have worked closely with many customers to implement their solutions and have already gained experience with blockchain technologies.
Our most relevant projects are, among others:
- SubIdentity (W3F Grant), Identity Directory for Substrate Chains
- Exchange for trading digital assets (Customer is a Top 200 Token of CMC)
- Token Swap WebApp (Customer is a Top 200 Token of CMC)
- [Blockchain, NFT Pallets & App](https://artists.niftymarket.com/) (In Development)

We look forward to contributing to the web3 ecosystem with an open-source project next.


### Team Code Repos

Source code will be in:
- https://github.com/TDSoftware

Team profiles:
- https://github.com/dobschal
  

### Team LinkedIn Profiles

- https://www.linkedin.com/company/tdsoftware-gmbh/mycompany/
- https://www.linkedin.com/in/dobschal/



## Development Status :open_book:

A concept and solution draft was created as part of this application and can be found in the Project Details chapter. 



## Development Roadmap :nut_and_bolt:

### Overview

- **Total Estimated Duration:**
- **Full-Time Equivalent (FTE):**
- **Total Costs:**

### Milestone 1 - Research and PoC implementation on upload part

- **Estimated duration: 2 months**
- **FTE: 2**
- **Costs:**

After the first research, the PoC pallet implementation will be developed. The goal of milestone 1, is a fully working round trip
(except redirect): a POC client reading a file, calling extrinsic, and uploading the content of a file, the CID information will be stored in the pallet,
then the uploaded file is verified by other IPFS tools.

 Number | Deliverable | Specification |
| -----: | ----------- | ------------- |
| 0a. | License | Apache 2.0 / GPLv3 / MIT / Unlicense |
| 0b. | Documentation | We will provide both **inline documentation** of the code and a basic **tutorial** that explains how a developer can re-use the implementation. |
| 0c.    | Testing |    Core functions will be covered by unit tests as far as reasonably applicable to ensure functionality and robustness. In the documentation, we will describe how to run these tests. |
| 1. | Implement ipfs upload extrinsic | The pallet implementation will be added, that allow bytes to uploads. |
| 2. | Implement POC client | The client can read data from file, call extrinsic and upload the content in bytes. |
| 3. | Verification | Verify the file uploaded |

### Milestone 2 -  PoC implementation on redirect part

- **Estimated Duration: 1 month** 
- **FTE:** 1**
- **Costs:**

The goal of the second milestone is to redirect utilities of substrate, a gRPC request can based on PRG mechanism redirect to any file server, which is not limited by IPFS.

 Number | Deliverable | Specification |
| -----: | ----------- | ------------- |
| 0a. | License | Apache 2.0 / GPLv3 / MIT / Unlicense |
| 0b. | Documentation | We will provide both **inline documentation** of the code and a basic **tutorial** that explains how a developer can re-use the implementation. |
| 0c.    | Testing |    Core functions will be covered by unit tests as far as reasonably applicable to ensure functionality and robustness. In the documentation, we will describe how to run these tests. |
| 1. | Implement | `#[prg(name = "nft_getArtworkById")]` will be designed and developed that allows users to redirect a request, which returns `Result<String>`, to a file server. |

### Milestone 3 - Integration and Benchmark

- **Estimated Duration: 2 months**
- **FTE: 2**
- **Costs:**

The goal of the third milestone is to have several features and APIs that cover potential use cases.

 Number | Deliverable | Specification |
| -----: | ----------- | ------------- |
| 0a. | License | Apache 2.0 / GPLv3 / MIT / Unlicense |
| 0b. | Documentation | We will provide both **inline documentation** of the code and a basic **tutorial** that explains how a developer can re-use the implementation. |
| 0c.    | Testing |    Core functions will be covered by unit tests as far as reasonably applicable to ensure functionality and robustness. In the documentation, we will describe how to run these tests. |
| 1. | Configure | The IPFS pallet implementation will be added with IPFS gateway in configure. |
| 2. | Query | The IPFS pallet can be queried and return a different version of CID as String. |
| 3. | Example | The example pallet can use IPFS pallet to store some data in HTML format in IPFS and provide gRPC to redirect requests to get the HTML content. |
| 4. | Benchmark | Benchmark on the size of the file the IPFS pallet can be accepted. |



## Additional Information :heavy_plus_sign:

This is our second application for an open-source project to innovate the web3 Ecosystem.
