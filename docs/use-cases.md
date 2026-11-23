# Use Case Specifications

## UC-01: Search Available Vehicles
- **Primary Actor:** Customer[span_9](start_span)[span_9](end_span)[span_10](start_span)[span_10](end_span)
- **Precondition:** Rental start date and end date are valid (start date <= end date, not in the past)[span_11](start_span)[span_11](end_span).
- **Main Flow:**
  1. Customer enters pickup date, return date, and optional vehicle type (e.g., Sedan, SUV, Electric)[span_12](start_span)[span_12](end_span)[span_13](start_span)[span_13](end_span).
  2. System checks fleet vehicles matching the criteria and their availability status[span_14](start_span)[span_14](end_span)[span_15](start_span)[span_15](end_span).
  3. System filters out vehicles with overlapping reservations for the requested date range[span_16](start_span)[span_16](end_span)[span_17](start_span)[span_17](end_span).
  4. System displays the list of available vehicles with daily/estimated prices[span_18](start_span)[span_18](end_span)[span_19](start_span)[span_19](end_span).
- **Alternative Flows:**
  - **A1 (No Vehicles Available):** No matching vehicles are free for the selected dates; system informs the customer and suggests alternative dates or vehicle types[span_20](start_span)[span_20](end_span).
  - **A2 (Invalid Date Range):** End date is earlier than start date or dates are invalid; system rejects the query and prompts for valid dates[span_21](start_span)[span_21](end_span).
- **Postcondition:** Customer views available vehicles for the requested period[span_22](start_span)[span_22](end_span).

## UC-02: Make Reservation
- **Primary Actor:** Customer[span_23](start_span)[span_23](end_span)[span_24](start_span)[span_24](end_span)
- **Precondition:** Customer has selected a valid date range and an available vehicle (FR-01, FR-02)[span_25](start_span)[span_25](end_span)[span_26](start_span)[span_26](end_span).
- **Main Flow:**
  1. Customer selects a vehicle and optionally chooses additional services (insurance, GPS, child seat)[span_27](start_span)[span_27](end_span)[span_28](start_span)[span_28](end_span).
  2. System verifies there are no overlapping reservations for the vehicle and date range[span_29](start_span)[span_29](end_span)[span_30](start_span)[span_30](end_span).
  3. System calculates the total price using the active pricing strategy and selected add-ons[span_31](start_span)[span_31](end_span)[span_32](start_span)[span_32](end_span)[span_33](start_span)[span_33](end_span).
  4. System creates a `Reservation` in `Pending` state and saves it[span_34](start_span)[span_34](end_span)[span_35](start_span)[span_35](end_span)[span_36](start_span)[span_36](end_span).
  5. System notifies observers (e.g., notification and audit log)[span_37](start_span)[span_37](end_span)[span_38](start_span)[span_38](end_span).
- **Alternative Flows:**
  - **A1 (Vehicle No Longer Available / Date Conflict):** Another reservation overlaps with the requested period; system blocks creation and raises a conflict error[span_39](start_span)[span_39](end_span)[span_40](start_span)[span_40](end_span).
  - **A2 (Customer Not Eligible / Missing Details):** Customer record or license rule is not satisfied; system prevents reservation creation[span_41](start_span)[span_41](end_span)[span_42](start_span)[span_42](end_span).
- **Postcondition:** A `Pending` reservation is recorded without double-booking the vehicle[span_43](start_span)[span_43](end_span)[span_44](start_span)[span_44](end_span)[span_45](start_span)[span_45](end_span)[span_46](start_span)[span_46](end_span).

## UC-03: Pay for Reservation
- **Primary Actor:** Customer[span_47](start_span)[span_47](end_span)[span_48](start_span)[span_48](end_span)
- **Precondition:** An eligible reservation exists in `Pending` state with a calculated total amount[span_49](start_span)[span_49](end_span)[span_50](start_span)[span_50](end_span)[span_51](start_span)[span_51](end_span).
- **Main Flow:**
  1. Customer initiates payment for the reservation[span_52](start_span)[span_52](end_span)[span_53](start_span)[span_53](end_span).
  2. System processes simulated payment and records a `Payment` / invoice[span_54](start_span)[span_54](end_span)[span_55](start_span)[span_55](end_span)[span_56](start_span)[span_56](end_span).
  3. Reservation transitions from `Pending` to `Confirmed` state[span_57](start_span)[span_57](end_span)[span_58](start_span)[span_58](end_span).
  4. System triggers notification and audit observers[span_59](start_span)[span_59](end_span)[span_60](start_span)[span_60](end_span).
- **Alternative Flows:**
  - **A1 (Payment Declined / Invalid Amount):** Simulated payment fails; reservation remains in `Pending` state and error is reported[span_61](start_span)[span_61](end_span)[span_62](start_span)[span_62](end_span).
  - **A2 (Invalid State Transition):** Payment is attempted on a `Cancelled` or `Completed` reservation; system rejects the operation[span_63](start_span)[span_63](end_span)[span_64](start_span)[span_64](end_span).
- **Postcondition:** Payment is recorded and reservation is in `Confirmed` state[span_65](start_span)[span_65](end_span)[span_66](start_span)[span_66](end_span)[span_67](start_span)[span_67](end_span)[span_68](start_span)[span_68](end_span).

## UC-04: Return Vehicle
- **Primary Actor:** Customer / Branch Staff[span_69](start_span)[span_69](end_span)[span_70](start_span)[span_70](end_span)
- **Precondition:** Reservation is in `Active` state (vehicle has been picked up)[span_71](start_span)[span_71](end_span)[span_72](start_span)[span_72](end_span).
- **Main Flow:**
  1. Customer or staff initiates vehicle return on or before the scheduled return date/time[span_73](start_span)[span_73](end_span)[span_74](start_span)[span_74](end_span).
  2. System checks whether the return is late[span_75](start_span)[span_75](end_span).
  3. System updates vehicle status back to `Available` (or `Maintenance` if damage is recorded) and transitions reservation to `Completed` state[span_76](start_span)[span_76](end_span)[span_77](start_span)[span_77](end_span)[span_78](start_span)[span_78](end_span)[span_79](start_span)[span_79](end_span).
  4. System generates/updates final summary and triggers observers[span_80](start_span)[span_80](end_span)[span_81](start_span)[span_81](end_span)[span_82](start_span)[span_82](end_span)[span_83](start_span)[span_83](end_span).
- **Alternative Flows:**
  - **A1 (Late Return):** Return occurs past the scheduled return time; system calculates a late return fee and adds it to the final charge before completing[span_84](start_span)[span_84](end_span)[span_85](start_span)[span_85](end_span).
  - **A2 (Invalid State):** Return is attempted when reservation is not `Active` (e.g., `Cancelled`); system rejects the transition[span_86](start_span)[span_86](end_span)[span_87](start_span)[span_87](end_span).
- **Postcondition:** Reservation is `Completed`, any late fee is recorded, and vehicle availability is updated[span_88](start_span)[span_88](end_span)[span_89](start_span)[span_89](end_span)[span_90](start_span)[span_90](end_span)[span_91](start_span)[span_91](end_span).

## UC-05: Cancel Reservation
- **Primary Actor:** Customer[span_92](start_span)[span_92](end_span)[span_93](start_span)[span_93](end_span)
- **Precondition:** Reservation exists in a cancellable state (e.g., `Pending` or `Confirmed`)[span_94](start_span)[span_94](end_span)[span_95](start_span)[span_95](end_span)[span_96](start_span)[span_96](end_span).
- **Main Flow:**
  1. Customer requests cancellation for an existing reservation[span_97](start_span)[span_97](end_span)[span_98](start_span)[span_98](end_span).
  2. System checks cancellation eligibility according to business rules[span_99](start_span)[span_99](end_span).
  3. Reservation transitions to `Cancelled` state and the date slot is released[span_100](start_span)[span_100](end_span)[span_101](start_span)[span_101](end_span)[span_102](start_span)[span_102](end_span).
  4. System triggers notification and audit observers[span_103](start_span)[span_103](end_span)[span_104](start_span)[span_104](end_span).
- **Alternative Flows:**
  - **A1 (Not Cancellable):** Reservation is already `Active` or `Completed` or `Cancelled`; system rejects the cancellation request[span_105](start_span)[span_105](end_span)[span_106](start_span)[span_106](end_span).
- **Postcondition:** Reservation is in `Cancelled` state and no longer blocks future bookings for that period[span_107](start_span)[span_107](end_span)[span_108](start_span)[span_108](end_span)[span_109](start_span)[span_109](end_span)[span_110](start_span)[span_110](end_span).
