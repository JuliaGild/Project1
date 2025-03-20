# Project1

USE al_Group_47114_G2;

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

CREATE TABLE Visit (
    visitID INT,
    dateVisited VARCHAR(45),
    patientID INT,
    staffID INT,
    PRIMARY KEY(visitID),
    FOREIGN KEY(patientID) REFERENCES Patient(patientID),
    FOREIGN KEY(staffID) REFERENCES Staff(staffID)
);

CREATE TABLE InsuranceProvider (
    providerID INT,
    providerName VARCHAR(45),
    PRIMARY KEY(providerID)
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

CREATE TABLE Storage (
    storageID INT,
    storageName VARCHAR(45),
    storageCapacity VARCHAR(45),
    PRIMARY KEY(storageID)
);

CREATE TABLE Payment (
    paymentID INT,
    paymentAmount VARCHAR(45),
    paymentMethod VARCHAR(45),
    billingID INT,
    PRIMARY KEY(paymentID),
    FOREIGN KEY(billingID) REFERENCES Billing(billingID)
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

CREATE TABLE Billing (
    billingID INT,
    billDescription VARCHAR(255),
    billAmt VARCHAR(45),
    statusID INT,
    patientID INT,
    PRIMARY KEY(billingID),
    FOREIGN KEY(patientID) REFERENCES Patient(patientID)
);
  
