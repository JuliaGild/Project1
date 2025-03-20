# Project 1 4610 Group Project 1

## Team Name
Group 2

## Team Members
- Julia Gild [@JuliaGild](https://github.com/JuliaGild)
- John Neely [@NeelyJohn](https://github.com/NeelyJohn)
- Valerie Tran [@ValerieTran](https://github.com/ValerieTran)
- Jack Glawatz [@jackglawatz](https://github.com/jackglawatz)
- Oluwabukola Ogundare [@RachaelOgundare](https://github.com/RachaelOgundare)

## Problem Description
The task for this project is to model and build a relational database as a multi-sector medical facility. Currently, the facility is running into record organization issues that ultimately result in billing delays, overlapping patient visits, and a lack of storage capacity. From this relational database, the facility hopes to streamline operations, improve efficiency, and provide accurate data tracking. This system should include the management of patients, medical staff members, appointments and schedules, billing requests, insurance claims, prescriptions and medications, and storage capacity. This database will, in turn, optimize the organization’s daily operations, improve patient care, and increase workflow efficiency.

## Data Model
### Explaination of data model:
This data model represents a hospital management system, detailing the relationships between patients, staff, medical records, billing, insurance, prescriptions, and storage. Patients visit the hospital, where they are attended to by staff members such as doctors and nurses. Their medical history, prescriptions, and visits are recorded in the system. Billing and insurance claims are tracked, ensuring proper financial management. The hospital also maintains an inventory of medicines and storage facilities, with a system in place for tracking the receipt and distribution of medical supplies. This model helps streamline hospital operations by organizing patient care, financial transactions, and resource management efficiently.
<img width="622" alt="Screenshot 2025-03-20 at 2 38 02 PM" src="https://github.com/user-attachments/assets/68b0ae8a-f690-4f2e-8200-9d60bf4afee1" />

## Data Model Dictionary
<img width="717" alt="Screenshot 2025-03-20 at 2 42 03 PM" src="https://github.com/user-attachments/assets/d1133be9-2596-4ec2-85d0-2d87747f9587" />
<img width="728" alt="Screenshot 2025-03-20 at 2 42 33 PM" src="https://github.com/user-attachments/assets/25608577-ffca-402f-aaa9-7de57a28e264" />
<img width="697" alt="Screenshot 2025-03-20 at 2 42 40 PM" src="https://github.com/user-attachments/assets/d14b8af3-cbde-4524-ad65-5c63ad2dfb95" />
<img width="690" alt="Screenshot 2025-03-20 at 2 42 46 PM" src="https://github.com/user-attachments/assets/9f278835-984f-4a59-b3bc-2f62adf5cb19" />
<img width="702" alt="Screenshot 2025-03-20 at 2 43 04 PM" src="https://github.com/user-attachments/assets/c4fec4b3-a77f-4c09-860f-ff133fee0ca4" />
<img width="703" alt="Screenshot 2025-03-20 at 2 43 09 PM" src="https://github.com/user-attachments/assets/53f843d6-9771-49c0-882e-f54c46a66a27" />
<img width="703" alt="Screenshot 2025-03-20 at 2 43 23 PM" src="https://github.com/user-attachments/assets/22b89ac5-1992-488e-bc95-547b2b930939" />
<img width="717" alt="Screenshot 2025-03-20 at 2 43 28 PM" src="https://github.com/user-attachments/assets/f8cf0371-f8d3-484b-857a-d08b2005e19e" />
<img width="707" alt="Screenshot 2025-03-20 at 2 43 39 PM" src="https://github.com/user-attachments/assets/40f70552-28a2-47fb-9c14-cf55bb564fd7" />
<img width="718" alt="Screenshot 2025-03-20 at 2 43 43 PM" src="https://github.com/user-attachments/assets/a2dac057-3d28-450e-97a8-4feb1647d191" />
<img width="646" alt="Screenshot 2025-03-20 at 2 43 48 PM" src="https://github.com/user-attachments/assets/20bc1a4a-0478-475e-91f7-1073a9385472" />
<img width="684" alt="Screenshot 2025-03-20 at 2 43 51 PM" src="https://github.com/user-attachments/assets/f3d8c251-ab15-44e3-a992-0e794c2ac986" />

## Relationships of Entities
<img width="529" alt="Screenshot 2025-03-20 at 2 49 09 PM" src="https://github.com/user-attachments/assets/7432ca69-5012-42dd-a546-b0fba4e2082e" />

## Forward Engineering Tables
CREATE TABLE Billing (
    billingID INT,
    billDescription VARCHAR(255),
    billAmt VARCHAR(45),
    statusID INT,
    patientID INT,
    PRIMARY KEY(billingID),
    FOREIGN KEY(patientID) REFERENCES Patient(patientID)
);

CREATE TABLE InsuranceClaim (
    claimID INT,
    claimPatient INT,
    claimDescription VARCHAR(255),
    claimDate VARCHAR(45),
    claimAmount VARCHAR(45),
    providerID INT,
    billingID INT,
    PRIMARY KEY(claimID),
    FOREIGN KEY(claimPatient) REFERENCES Patient(patientID),
    FOREIGN KEY(providerID) REFERENCES InsuranceProvider(providerID),
    FOREIGN KEY(billingID) REFERENCES Billing(billingID)
);

CREATE TABLE InsuranceProvider (
    providerID INT,
    providerName VARCHAR(45),
    PRIMARY KEY(providerID)
);

CREATE TABLE Medicine (
    medicineID INT,
    medicineName VARCHAR(45),
    recommendedMedicineDosage VARCHAR(45),
    medicineManufacturer VARCHAR(45),
    prescriptionID INT,
    patientID INT,
    PRIMARY KEY(medicineID),
    FOREIGN KEY(prescriptionID) REFERENCES Prescription(prescriptionID),
    FOREIGN KEY(patientID) REFERENCES Patient(patientID)
);

CREATE TABLE Patient (
    patientID INT,
    patientName VARCHAR(45),
    patientHistory VARCHAR(255),
    patientBday VARCHAR(45),
    patientGender VARCHAR(45),
    patientPhone VARCHAR(45),
    providerID INT,
    PRIMARY KEY(patientID),
    FOREIGN KEY(providerID) REFERENCES InsuranceProvider(providerID)
);

CREATE TABLE Payment (
    paymentID INT,
    paymentAmount VARCHAR(45),
    paymentMethod VARCHAR(45),
    billingID INT,
    PRIMARY KEY(paymentID),
    FOREIGN KEY(billingID) REFERENCES Billing(billingID)
);

CREATE TABLE Prescription (
    prescriptionID INT,
    dosageAmt VARCHAR(45),
    frequency VARCHAR(45),
    patientID INT,
    staffID INT,
    roomID INT,
    PRIMARY KEY(prescriptionID),
    FOREIGN KEY(patientID) REFERENCES Patient(patientID),
    FOREIGN KEY(staffID) REFERENCES Staff(staffID),
    FOREIGN KEY(roomID) REFERENCES Schedule(roomID)
);

CREATE TABLE ReceiptOfStorage (
    receiptID INT,
    medicineID INT,
    storageID INT,
    dosageReceived INT,
    PRIMARY KEY(receiptID),
    FOREIGN KEY(medicineID) REFERENCES Medicine(medicineID),
    FOREIGN KEY(storageID) REFERENCES Storage(storageID)
);

CREATE TABLE Schedule (
    roomID INT,
    doctorID INT,
    nurseID INT,
    onCallStatus VARCHAR(45),
    shiftNotes VARCHAR(255),
    PRIMARY KEY(roomID),
    FOREIGN KEY(doctorID) REFERENCES Staff(staffID),
    FOREIGN KEY(nurseID) REFERENCES Staff(staffID)
);

CREATE TABLE Staff (
    staffID INT,
    staffName VARCHAR(45),
    staffRole VARCHAR(45),
    staffNumber VARCHAR(45),
    staffDOB VARCHAR(45),
    staffGender VARCHAR(45),
    billing VARCHAR(45),
    roomID INT,
    PRIMARY KEY(staffID),
    FOREIGN KEY(roomID) REFERENCES Schedule(roomID)
);

CREATE TABLE Storage (
    storageID INT,
    storageName VARCHAR(45),
    storageCapacity VARCHAR(45),
    PRIMARY KEY(storageID)
);

CREATE TABLE Visit (
    visitID INT,
    dateVisited VARCHAR(45),
    patientID INT,
    staffID INT,
    PRIMARY KEY(visitID),
    FOREIGN KEY(patientID) REFERENCES Patient(patientID),
    FOREIGN KEY(staffID) REFERENCES Staff(staffID)
);

## Query Check Box
<img width="589" alt="Screenshot 2025-03-20 at 2 53 43 PM" src="https://github.com/user-attachments/assets/016548f8-5228-4b0c-96f6-b75a2f6d2c78" />

## Queries
### Complex
1. Query 1: List the total billing amount for each patient along with the number of payments they have made.![Query 1](https://github.com/user-attachments/assets/040bab2f-13ee-459e-b880-b2facc89553b)
This query provides valuable insights into patient billing and payment behavior by calculating the total billing amount for each patient and tracking the number of payments they have made. The total billing amount reveals how much a patient has been charged overall, giving the hospital a clear view of their financial responsibility. Meanwhile, the number of payments indicates how actively a patient has been addressing their bills. This information is particularly useful for identifying patients who may be at financial risk, especially if they have a high total billing amount but few payments recorded. Additionally, tracking payment patterns can help the hospital predict cash flow, manage collections more effectively, and prioritize follow-up actions for patients who may require financial guidance or support.

3. 






