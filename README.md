# Certification Smart Contract
This Solidity smart contract implements a decentralized certification platform, enabling the generation, storage, and verification of certificates on the blockchain.
The contract uses require, revert, and assert methods to ensure security, validation, and state verification.
## Contract Description:

### Structure

#### •	stuID: The student's ID
#### •	stuName: The student's name
#### •	courseName: The name of the course for which the certificate is issued
#### •	authName: The name of the authority issuing the certificate
#### •	hashID: A unique identifier to store the certificate's data

### Functions
#### •	generateCertificate
Generates a new certificate with the provided details.
Ensures the certificate ID is unique using require.
Stores the certificate in a mapping.
#### •	getCertificate
Retrieves the certificate data for a given certificate ID.
Uses revert to handle the case where the certificate does not exist..
#### •	isVerified
Checks if a certificate exists and is verified.
Uses assert to ensure the certificate's hash is not empty.

## Getting Started

### Installing

•	Simply search for remix.ethereum.org in your web browser.	No installation is required.

### Executing program
• Open Remix IDE in your browser. Create a New File with .sol extention. Copy and paste the following code into the file:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.13;

contract Certification {
    struct Certificate {
        string stuID;           // student ID
        string stuName;        // student name
        string courseName;    // course name for certificate to be generated
        string authName;      //Name of autthority issueing certificate
        string hashID;        // unique identity to store certificate's data
    }

    mapping(string => Certificate) public certificates;
    

    function generateCertificate(
        string memory certificate_id,
        string memory stu_ID,
        string memory stu_Name,
        string memory course_Name,
        string memory auth_Name,
        string memory hash_ID
    ) public {
        // Check if certificate with the given ID already exists
        require(bytes(certificates[certificate_id].hashID).length == 0,
            "Certificate with this ID already exists"
        );

        // Creating the certificate
        Certificate memory cert = Certificate({
            stuID: stu_ID,
            stuName: stu_Name,
            courseName: course_Name,
            authName: auth_Name,
            hashID: hash_ID
        });

        // Storing the certificate in the mapping
        certificates[certificate_id] = cert;

    }

    function getCertificate(string memory certificate_id) public view returns (
        string memory stu_ID,
        string memory stu_Name,
        string memory course_Name,
        string memory auth_Name,
        string memory hash_ID
    ) {
        Certificate memory cert = certificates[certificate_id];

        // Checking if the certificate with the given ID exists
        if (bytes(certificates[certificate_id].hashID).length == 0) {
            revert("Certificate with this ID does not exist");
        }

        // Return the values from the certificate
        return (
            cert.stuID,
            cert.stuName,
            cert.courseName,
            cert.authName,
            cert.hashID
        );
    }

    function isVerified(
        string memory certificate_id
    ) public view returns (bool) {
        Certificate storage cert = certificates[certificate_id];
        // Use assert to ensure the certificate's hash is not empty
        assert(bytes(cert.hashID).length != 0);
        return true;
    }

}

```
Compile and then deploy the Contract. Call generateCertificate with the appropriate parameters to create a new certificate.
Use getCertificate to fetch the details of a certificate using its ID.
Call isVerified to check if a certificate with a given ID exists and is valid.

## Authors

Gurleen Kaur
(@https://github.com/gurleenkaur0703)

## License

This project is licensed under the MIT License.
