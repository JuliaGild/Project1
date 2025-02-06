# Project1

USE al_Group_47114_G2;
CREATE TABLE Patient (
  patientID INT,
  patientName VARCHAR(45),
  patientMedHistory VARCHAR(45),
  patientBirthDay VARCHAR(45),
  patientGender VARCHAR(45),
  patientPhoneNumber VARCHAR(45),
  providerID VARCHAR(45),
  PRIMARY KEY (patientID));


CREATE TABLE Staff (
  staffID INT NOT NULL,
  staffName VARCHAR(45),
  staffRole VARCHAR(45),
  staffNumber VARCHAR(45),
  staffDOB VARCHAR(45),
  staffGender VARCHAR(45),
  PRIMARY KEY (staffID));


CREATE TABLE Visit (
  visitID INT,
  patientID VARCHAR(45),
  dateVisit VARCHAR(45),
  providerID VARCHAR(45),
  PRIMARY KEY (visitID));


CREATE TABLE Billing (
  billID INT,
  billDescripton VARCHAR(45),
  billAmount VARCHAR(45),
  patientID VARCHAR(45),
  providerID VARCHAR(45),
  statusID VARCHAR(45),
  PRIMARY KEY (billID));


CREATE TABLE Medicine (
  medicineID INT,
  medicineName VARCHAR(45),
  medicineDosage VARCHAR(45),
  medicineManufacturer VARCHAR(45),
  PRIMARY KEY (medicineID));


CREATE TABLE Prescription (
  prescriptionID INT,
  patientID VARCHAR(45),
  medicineID VARCHAR(45),
  dosageAmt VARCHAR(45),
  frequency VARCHAR(45),
  providerID VARCHAR(45),
  PRIMARY KEY (prescriptionID));


CREATE TABLE Inventory (
  quantityOnHand INT,
  itemID VARCHAR(45),
  itemName VARCHAR(45),
  itemDescription VARCHAR(45),
  category VARCHAR(45),
  unitCost VARCHAR(45),
  PRIMARY KEY (quantityOnHand));



CREATE TABLE InsuranceProvider (
  providerID INT,
  providerName VARCHAR(45),
  PRIMARY KEY (providerID));


CREATE TABLE InsuranceClaim (
  claimID INT,
  claimPatient VARCHAR(45),
  claimDescription VARCHAR(45),
  claimDate VARCHAR(45),
  claimAmount VARCHAR(45),
  PRIMARY KEY (claimID));

CREATE TABLE Payment (
  paymentID INT,
  paymentAmount VARCHAR(45),
  paymentMethod VARCHAR(45),
  billID VARCHAR(45),
  PRIMARY KEY (paymentID));


CREATE TABLE OfficeSchedule (
  roomID INT,
  doctorID VARCHAR(45),
  nurseID VARCHAR(45),
  onCallStatus VARCHAR(45),
  shiftNotes VARCHAR(45),
  PRIMARY KEY (roomID));


CREATE TABLE ServiceUsage (
  serviceID INT,
  UsageID VARCHAR(45),
  PRIMARY KEY (serviceID));
  
