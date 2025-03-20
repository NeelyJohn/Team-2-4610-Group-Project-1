# Team-2-4610-Group-Project-1

Group 2

Team Members
Julia Gild @JuliaGild
John Neely @NeelyJohn
Valerie Tran @ValerieTran
Jack Glawatz @jackglawatz
Oluwabukola Ogundare @RachaelOgundare
Problem Description
The task for this project is to model and build a relational database as a multi-sector medical facility. Currently, the facility is running into record organization issues that ultimately result in billing delays, overlapping patient visits, and a lack of storage capacity. From this relational database, the facility hopes to streamline operations, improve efficiency, and provide accurate data tracking. This system should include the management of patients, medical staff members, appointments and schedules, billing requests, insurance claims, prescriptions and medications, and storage capacity. This database will, in turn, optimize the organization’s daily operations, improve patient care, and increase workflow efficiency.

Data Model
Explaination of data model:
This data model represents a hospital management system, detailing the relationships between patients, staff, medical records, billing, insurance, prescriptions, and storage. Patients visit the hospital, where they are attended to by staff members such as doctors and nurses. Their medical history, prescriptions, and visits are recorded in the system. Billing and insurance claims are tracked, ensuring proper financial management. The hospital also maintains an inventory of medicines and storage facilities, with a system in place for tracking the receipt and distribution of medical supplies. This model helps streamline hospital operations by organizing patient care, financial transactions, and resource management efficiently. Screenshot 2025-03-20 at 2 38 02 PM

Data Model Dictionary
Screenshot 2025-03-20 at 2 42 03 PM Screenshot 2025-03-20 at 2 42 33 PM Screenshot 2025-03-20 at 2 42 40 PM Screenshot 2025-03-20 at 2 42 46 PM Screenshot 2025-03-20 at 2 43 04 PM Screenshot 2025-03-20 at 2 43 09 PM Screenshot 2025-03-20 at 2 43 23 PM Screenshot 2025-03-20 at 2 43 28 PM Screenshot 2025-03-20 at 2 43 39 PM Screenshot 2025-03-20 at 2 43 43 PM Screenshot 2025-03-20 at 2 43 48 PM Screenshot 2025-03-20 at 2 43 51 PM
Relationships of Entities
Screenshot 2025-03-20 at 2 49 09 PM
Forward Engineering Tables
CREATE TABLE Billing ( billingID INT, billDescription VARCHAR(255), billAmt VARCHAR(45), statusID INT, patientID INT, PRIMARY KEY(billingID), FOREIGN KEY(patientID) REFERENCES Patient(patientID) );

CREATE TABLE InsuranceClaim ( claimID INT, claimPatient INT, claimDescription VARCHAR(255), claimDate VARCHAR(45), claimAmount VARCHAR(45), providerID INT, billingID INT, PRIMARY KEY(claimID), FOREIGN KEY(claimPatient) REFERENCES Patient(patientID), FOREIGN KEY(providerID) REFERENCES InsuranceProvider(providerID), FOREIGN KEY(billingID) REFERENCES Billing(billingID) );

CREATE TABLE InsuranceProvider ( providerID INT, providerName VARCHAR(45), PRIMARY KEY(providerID) );

CREATE TABLE Medicine ( medicineID INT, medicineName VARCHAR(45), recommendedMedicineDosage VARCHAR(45), medicineManufacturer VARCHAR(45), prescriptionID INT, patientID INT, PRIMARY KEY(medicineID), FOREIGN KEY(prescriptionID) REFERENCES Prescription(prescriptionID), FOREIGN KEY(patientID) REFERENCES Patient(patientID) );

CREATE TABLE Patient ( patientID INT, patientName VARCHAR(45), patientHistory VARCHAR(255), patientBday VARCHAR(45), patientGender VARCHAR(45), patientPhone VARCHAR(45), providerID INT, PRIMARY KEY(patientID), FOREIGN KEY(providerID) REFERENCES InsuranceProvider(providerID) );

CREATE TABLE Payment ( paymentID INT, paymentAmount VARCHAR(45), paymentMethod VARCHAR(45), billingID INT, PRIMARY KEY(paymentID), FOREIGN KEY(billingID) REFERENCES Billing(billingID) );

CREATE TABLE Prescription ( prescriptionID INT, dosageAmt VARCHAR(45), frequency VARCHAR(45), patientID INT, staffID INT, roomID INT, PRIMARY KEY(prescriptionID), FOREIGN KEY(patientID) REFERENCES Patient(patientID), FOREIGN KEY(staffID) REFERENCES Staff(staffID), FOREIGN KEY(roomID) REFERENCES Schedule(roomID) );

CREATE TABLE ReceiptOfStorage ( receiptID INT, medicineID INT, storageID INT, dosageReceived INT, PRIMARY KEY(receiptID), FOREIGN KEY(medicineID) REFERENCES Medicine(medicineID), FOREIGN KEY(storageID) REFERENCES Storage(storageID) );

CREATE TABLE Schedule ( roomID INT, doctorID INT, nurseID INT, onCallStatus VARCHAR(45), shiftNotes VARCHAR(255), PRIMARY KEY(roomID), FOREIGN KEY(doctorID) REFERENCES Staff(staffID), FOREIGN KEY(nurseID) REFERENCES Staff(staffID) );

CREATE TABLE Staff ( staffID INT, staffName VARCHAR(45), staffRole VARCHAR(45), staffNumber VARCHAR(45), staffDOB VARCHAR(45), staffGender VARCHAR(45), billing VARCHAR(45), roomID INT, PRIMARY KEY(staffID), FOREIGN KEY(roomID) REFERENCES Schedule(roomID) );

CREATE TABLE Storage ( storageID INT, storageName VARCHAR(45), storageCapacity VARCHAR(45), PRIMARY KEY(storageID) );

CREATE TABLE Visit ( visitID INT, dateVisited VARCHAR(45), patientID INT, staffID INT, PRIMARY KEY(visitID), FOREIGN KEY(patientID) REFERENCES Patient(patientID), FOREIGN KEY(staffID) REFERENCES Staff(staffID) );

Query Check Box
Screenshot 2025-03-20 at 2 53 43 PM
Queries
Complex
C- Query 1: List the total billing amount for each patient along with the number of payments they have made.
Query 1
This query provides valuable insights into patient billing and payment behavior by calculating the total billing amount for each patient and tracking the number of payments they have made. The total billing amount reveals how much a patient has been charged overall, giving the hospital a clear view of their financial responsibility. Meanwhile, the number of payments indicates how actively a patient has been addressing their bills. This information is particularly useful for identifying patients who may be at financial risk, especially if they have a high total billing amount but few payments recorded. Additionally, tracking payment patterns can help the hospital predict cash flow, manage collections more effectively, and prioritize follow-up actions for patients who may require financial guidance or support.

C- Query 2: List the storage facilities that are nearing capacity.
Q2
This query identifies which storage facilities are approaching their maximum capacity, providing crucial information for inventory management. By highlighting facilities that are nearly full, the hospital can take proactive measures such as redistributing supplies, adjusting delivery schedules, or planning for additional storage space. Monitoring storage levels is essential to ensure that medical supplies, medications, and equipment are always available without risking overstocking or space constraints. Identifying these trends early helps maintain operational efficiency and prevents potential disruptions in patient care due to supply shortages

C- Query 3: List Patients and Payment Details if they have made more than one payment.
Screenshot 2025-03-20 at 3 05 19 PM
This query identifies patients who have made more than one payment. The goal is to help the healthcare system track patients with multiple transactions, which may indicate ongoing treatments, installment plans, or potential billing issues. This information supports better financial management, follow-up strategies, and ensures patients receive appropriate care without financial oversight.

C- Query 4: List the patient's name and ID number who are identified as High-Risk Patients (Unpaid Bills + Frequent Visits). To be considered High-Risk, patients have to have both 3+ unpaid bills and 4+ visits.
Screenshot 2025-03-20 at 3 07 11 PM
This SQL query helps the hospital identify high-risk patients by pinpointing those with 3 or more unpaid bills and 4 or more visits. Filtering for unpaid bills ensures that only patients with outstanding payments are considered, while grouping the data by patient and counting their records highlights those frequently visiting the hospital. This information is crucial for the hospital's billing department to prioritize overdue accounts and follow up with patients who may require financial support. Additionally, identifying frequent visitors enables care teams to provide better case management, chronic care planning, or social work services to improve patient outcomes. Overall, this query enhances the hospital’s ability to manage resources efficiently while addressing both financial risks and patient care needs.

C- Query 5: List Patients name, ID, visit date, and visit ID if they have overlapping two or more visits on the same day.
Screenshot 2025-03-20 at 3 07 57 PM
This query helps find patients who might need extra attention or care. For example, if someone visits multiple times in a day, it could mean they have a serious health problem that needs quick treatment, like in emergencies. Also, if patients come back for check-ups after a procedure, it might be because of complications or more tests needed. By spotting these patterns, the hospital can improve how it schedules appointments, manages resources, and follows up with patients, leading to better care and outcomes for those with urgent or complex needs.

C- Query 6: Retrieve the latest prescription for each patient and list the medicine name, dosage amount and frequency of the medicine.
Screenshot 2025-03-20 at 3 08 35 PM
This query is designed to retrieve the most recent prescription for each patient by utilizing a correlated subquery. The outer query selects patient details along with prescription information, ensuring the data is relevant to the correct individual. The inner subquery plays a key role by identifying the maximum prescriptionID for each patient, which represents the most recent prescription, assuming prescription IDs increase over time. The WHERE condition ensures that only the latest prescription is included in the final result. This approach is especially useful in healthcare systems for tracking current medication records, ensuring medical staff have access to the most up-to-date prescription information, which helps improve patient care and reduces the risk of administering outdated treatments.

C- Query 7: List patients whose medical history includes specific procedures related to "Control Bleeding" or any kind of "Alteration.
Screenshot 2025-03-20 at 3 09 16 PM
The query retrieves patients whose medical history includes procedures related to "Control Bleeding" or "Alteration" by using a regular expression (REGEXP) filter. The result set displays patient IDs, names, and relevant patient history entries, ensuring that only records matching the specified keywords appear. This approach is useful for quickly identifying patients who have undergone specific procedures, helping medical staff analyze trends, provide targeted treatments, and streamline decision-making.

C- Query 8: Identify patients who have never filed an insurance claim.
Screenshot 2025-03-20 at 3 10 07 PM
The hospital uses this query to identify patients who have never filed an insurance claim, helping staff understand who may be paying out-of-pocket or not utilizing their insurance benefits. This allows the hospital to provide financial guidance, assist with claim filing, and ensure patients are aware of available coverage. By analyzing this data, the hospital can improve billing efficiency, enhance patient support programs, and reduce the risk of missed reimbursements.

Simple
S- Query 1: Find patients with a claim amount greater than the average claim amount of their insurance provider.
Screenshot 2025-03-20 at 3 10 51 PM
This query helps the hospital flag patients whose claims are significantly higher than the average for their insurance provider. If a patient has a higher-than-average claim, it could mean they have a more complex medical condition requiring additional care or specialized treatment. For example, if a patient consistently has high claims, they might have ongoing health issues that need closer monitoring. It could also help identify potential billing discrepancies, ensuring accurate claims and preventing overcharges. By spotting these patterns, the hospital can improve financial planning, optimize resource allocation, and enhance patient care for those with complex medical needs.

S- Query 2: Count the number of insurance claims filed by each patient.
Screenshot 2025-03-20 at 3 11 30 PM
This query helps the hospital understand patient interaction with insurance claims. Seeing how many claims each patient files can reveal patterns in hospital visits and treatment needs. For example, patients with frequent claims may rely heavily on medical services, which could indicate a need for better care coordination or alternative treatment plans. It also helps in managing administrative workloads by identifying high-volume claim processing areas. With this information, the hospital can streamline operations, improve patient experience, and ensure smoother insurance processing.
