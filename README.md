

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ATENEO DE NAGA UNIVERSITY - Gate Pass Application</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            background-color: #f0f4f8;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        .form-container {
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
        }
        .university-blue {
            background-color: #003366;
        }
        .university-gold {
            color: #FFD700;
        }
        select {
            background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' fill='none' viewBox='0 0 20 20'%3e%3cpath stroke='%236b7280' stroke-linecap='round' stroke-linejoin='round' stroke-width='1.5' d='M6 8l4 4 4-4'/%3e%3c/svg%3e");
            background-position: right 0.5rem center;
            background-repeat: no-repeat;
            background-size: 1.5em 1.5em;
            padding-right: 2.5rem;
            -webkit-appearance: none;
            -moz-appearance: none;
            appearance: none;
        }
        .btn-submit {
            background-color: #003366;
            transition: all 0.3s ease;
        }
        .btn-submit:hover {
            background-color: #002244;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
        .error-message {
            color: #e53e3e;
            font-size: 0.875rem;
            margin-top: 0.25rem;
        }
        .input-error {
            border-color: #e53e3e !important;
        }
        .section-error {
            border-left: 4px solid #e53e3e;
            padding-left: 1rem;
            background-color: #fff5f5;
        }
        .verified-email {
            position: relative;
        }
        .verified-badge {
            position: absolute;
            right: 10px;
            top: 50%;
            transform: translateY(-50%);
            color: #10B981;
            display: none;
        }
        .verified-badge.active {
            display: block;
        }
        .application-summary {
            background-color: #f8fafc;
            border: 1px solid #e2e8f0;
            border-radius: 0.5rem;
            padding: 1.5rem;
            margin-top: 2rem;
        }
        .summary-item {
            display: flex;
            margin-bottom: 0.75rem;
        }
        .summary-label {
            font-weight: 600;
            width: 40%;
            color: #4a5568;
        }
        .summary-value {
            width: 60%;
        }
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 50;
        }
        .modal-content {
            background-color: white;
            border-radius: 0.5rem;
            max-width: 90%;
            width: 600px;
            max-height: 90vh;
            overflow-y: auto;
        }
        @media print {
            body * {
                visibility: hidden;
            }
            #printSummary, #printSummary * {
                visibility: visible;
            }
            #printSummary {
                position: absolute;
                left: 0;
                top: 0;
                width: 100%;
            }
            .no-print {
                display: none !important;
            }
        }
    </style>
</head>
<body>
    <div class="min-h-screen flex flex-col items-center py-8 px-4">
        <!-- Header -->
        <div class="w-full max-w-4xl mb-8 text-center">
            <div class="university-blue rounded-lg py-6 px-4">
                <h1 class="text-3xl md:text-4xl font-bold text-white">ATENEO DE NAGA UNIVERSITY</h1>
                <p class="university-gold mt-2 text-xl font-semibold">Gate Pass Application</p>
            </div>
        </div>
        
        <!-- Main Content -->
        <div class="w-full max-w-4xl bg-white rounded-lg p-6 md:p-8 form-container">
            <form id="gatePassForm" onsubmit="submitForm(event)">
                <!-- Form Validation Error Message -->
                <div id="formErrorMessage" class="hidden mb-6 p-4 bg-red-100 border border-red-400 text-red-700 rounded-md">
                    <p class="font-medium">Please complete all required fields before submitting.</p>
                    <p class="mt-2">Scroll down to see the highlighted sections that need your attention.</p>
                </div>
                
                <!-- Duplicate ID Error Message -->
                <div id="duplicateIdMessage" class="hidden mb-6 p-4 bg-red-100 border border-red-400 text-red-700 rounded-md">
                    <p class="font-medium">This ID Number has already been used.</p>
                    <p class="mt-2">Please use a different ID number or contact the Security Office for assistance.</p>
                </div>
                
                <!-- Applicant's Information Section -->
                <div id="applicantSection" class="mb-8">
                    <h2 class="text-xl font-bold text-[#003366] mb-6 uppercase">APPLICANT'S INFORMATION</h2>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="md:col-span-2">
                            <label for="applicantName" class="block text-sm font-medium text-gray-700 mb-2">Applicant's Full Name: <span class="text-red-600">*</span></label>
                            <input type="text" id="applicantName" name="applicantName" required
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="applicantName-error">Please enter your full name</div>
                        </div>
                        <div>
                            <label for="driversLicense" class="block text-sm font-medium text-gray-700 mb-2">Driver's License: <span class="text-red-600">*</span></label>
                            <input type="text" id="driversLicense" name="driversLicense" required
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="driversLicense-error">Please enter your driver's license number</div>
                        </div>
                        <div>
                            <label for="applicantContact" class="block text-sm font-medium text-gray-700 mb-2">Contact Number: <span class="text-red-600">*</span></label>
                            <input type="tel" id="applicantContact" name="applicantContact" required
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="applicantContact-error">Please enter your contact number</div>
                        </div>
                        <div class="verified-email">
                            <label for="applicantEmail" class="block text-sm font-medium text-gray-700 mb-2">Email Address: <span class="text-red-600">*</span></label>
                            <div class="relative">
                                <input type="email" id="applicantEmail" name="applicantEmail" required
                                    class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]"
                                    onblur="validateEmail(this)">
                                <span class="verified-badge" id="applicantEmail-verified">
                                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                                        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
                                    </svg>
                                </span>
                            </div>
                            <div class="error-message hidden" id="applicantEmail-error">Please enter a valid email address</div>
                        </div>
                        <div class="md:col-span-2">
                            <label for="address" class="block text-sm font-medium text-gray-700 mb-2">Address: <span class="text-red-600">*</span></label>
                            <input type="text" id="address" name="address" required
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="address-error">Please enter your address</div>
                        </div>
                    </div>
                </div>
                
                <!-- Affiliation Section -->
                <div id="affiliationSection" class="mb-8">
                    <h2 class="text-xl font-bold text-[#003366] mb-6 uppercase">AFFILIATION WITH THE UNIVERSITY</h2>
                    
                    <div class="mb-4">
                        <label for="affiliation" class="block text-sm font-medium text-gray-700 mb-2">Select your affiliation: <span class="text-red-600">*</span></label>
                        <select id="affiliation" name="affiliation" required onchange="toggleAffiliationSections()"
                            class="w-full px-4 py-3 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366] text-gray-700">
                            <option value="" selected disabled>-- Select your affiliation --</option>
                            <option value="student">Student/Parent - P 230.00</option>
                            <option value="employee">Employee - P 230.00</option>
                            <option value="concessionaire">Concessionaire/Delivery - P 600.00</option>
                        </select>
                        <div class="error-message hidden" id="affiliation-error">Please select your affiliation</div>
                    </div>
                </div>
                
                <!-- Student's Information Section -->
                <div id="studentSection" class="mb-8 hidden">
                    <h2 class="text-xl font-bold text-[#003366] mb-6 uppercase">STUDENT'S INFORMATION</h2>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label for="studentName" class="block text-sm font-medium text-gray-700 mb-2">Student's Full Name: <span class="text-red-600">*</span></label>
                            <input type="text" id="studentName" name="studentName"
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="studentName-error">Please enter student's full name</div>
                        </div>
                        <div>
                            <label for="studentId" class="block text-sm font-medium text-gray-700 mb-2">Student's ID Number: <span class="text-red-600">*</span></label>
                            <input type="text" id="studentId" name="studentId" onblur="checkDuplicateId(this)"
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="studentId-error">Please enter student's ID number</div>
                            <div class="error-message hidden" id="studentId-duplicate-error">This ID Number has already been used</div>
                        </div>
                        <div>
                            <label for="studentContact" class="block text-sm font-medium text-gray-700 mb-2">Contact Number: <span class="text-red-600">*</span></label>
                            <input type="tel" id="studentContact" name="studentContact"
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="studentContact-error">Please enter student's contact number</div>
                        </div>
                        <div class="verified-email">
                            <label for="studentEmail" class="block text-sm font-medium text-gray-700 mb-2">Email Address: <span class="text-red-600">*</span></label>
                            <div class="relative">
                                <input type="email" id="studentEmail" name="studentEmail"
                                    class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]"
                                    onblur="validateEmail(this)">
                                <span class="verified-badge" id="studentEmail-verified">
                                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                                        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
                                    </svg>
                                </span>
                            </div>
                            <div class="error-message hidden" id="studentEmail-error">Please enter a valid email address</div>
                        </div>
                        <div>
                            <label for="yearLevel" class="block text-sm font-medium text-gray-700 mb-2">Student's Year/Level: <span class="text-red-600">*</span></label>
                            <input type="text" id="yearLevel" name="yearLevel"
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="yearLevel-error">Please enter student's year/level</div>
                        </div>
                        <div>
                            <label for="course" class="block text-sm font-medium text-gray-700 mb-2">Academic Program: <span class="text-red-600">*</span></label>
                            <select id="course" name="course"
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                                <option value="" selected disabled>-- Select academic program --</option>
                                <option value="aclc">ACLC</option>
                                <option value="grade_school">Grade School</option>
                                <option value="junior_high">Junior High School</option>
                                <option value="senior_high">Senior High School</option>
                                <option value="college">College</option>
                                <option value="law">College of Law</option>
                                <option value="graduate">Graduate School</option>
                            </select>
                            <div class="error-message hidden" id="course-error">Please select an academic program</div>
                        </div>
                    </div>
                </div>
                
                <!-- Employee's Information Section -->
                <div id="employeeSection" class="mb-8 hidden">
                    <h2 class="text-xl font-bold text-[#003366] mb-6 uppercase">EMPLOYEE'S INFORMATION</h2>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label for="employeeName" class="block text-sm font-medium text-gray-700 mb-2">Employee's Full Name: <span class="text-red-600">*</span></label>
                            <input type="text" id="employeeName" name="employeeName"
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="employeeName-error">Please enter employee's full name</div>
                        </div>
                        <div>
                            <label for="employeeId" class="block text-sm font-medium text-gray-700 mb-2">Employee's ID Number: <span class="text-red-600">*</span></label>
                            <input type="text" id="employeeId" name="employeeId" onblur="checkDuplicateId(this)"
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="employeeId-error">Please enter employee's ID number</div>
                            <div class="error-message hidden" id="employeeId-duplicate-error">This ID Number has already been used</div>
                        </div>
                        <div>
                            <label for="employeeContact" class="block text-sm font-medium text-gray-700 mb-2">Contact Number: <span class="text-red-600">*</span></label>
                            <input type="tel" id="employeeContact" name="employeeContact"
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="employeeContact-error">Please enter employee's contact number</div>
                        </div>
                        <div class="verified-email">
                            <label for="employeeEmail" class="block text-sm font-medium text-gray-700 mb-2">Email Address: <span class="text-red-600">*</span></label>
                            <div class="relative">
                                <input type="email" id="employeeEmail" name="employeeEmail"
                                    class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]"
                                    onblur="validateEmail(this)">
                                <span class="verified-badge" id="employeeEmail-verified">
                                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                                        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
                                    </svg>
                                </span>
                            </div>
                            <div class="error-message hidden" id="employeeEmail-error">Please enter a valid email address</div>
                        </div>
                        <div>
                            <label for="department" class="block text-sm font-medium text-gray-700 mb-2">Department/Office: <span class="text-red-600">*</span></label>
                            <input type="text" id="department" name="department"
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="department-error">Please enter department/office</div>
                        </div>
                        <div>
                            <label for="position" class="block text-sm font-medium text-gray-700 mb-2">Position/Designation: <span class="text-red-600">*</span></label>
                            <input type="text" id="position" name="position"
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="position-error">Please enter position/designation</div>
                        </div>
                    </div>
                </div>
                
                <!-- Concessionaire/Delivery Section -->
                <div id="concessionaireSection" class="mb-8 hidden">
                    <h2 class="text-xl font-bold text-[#003366] mb-6 uppercase">CONCESSIONAIRE/DELIVERY INFORMATION</h2>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label for="companyName" class="block text-sm font-medium text-gray-700 mb-2">Company/Business Name: <span class="text-red-600">*</span></label>
                            <input type="text" id="companyName" name="companyName"
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="companyName-error">Please enter company/business name</div>
                        </div>
                        <div>
                            <label for="businessType" class="block text-sm font-medium text-gray-700 mb-2">Type of Business/Service: <span class="text-red-600">*</span></label>
                            <input type="text" id="businessType" name="businessType"
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="businessType-error">Please enter type of business/service</div>
                        </div>
                        <div>
                            <label for="contactNumber" class="block text-sm font-medium text-gray-700 mb-2">Contact Number: <span class="text-red-600">*</span></label>
                            <input type="tel" id="contactNumber" name="contactNumber"
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="contactNumber-error">Please enter contact number</div>
                        </div>
                    </div>
                </div>
                
                <!-- Vehicle Information Section -->
                <div id="vehicleSection" class="mb-8 hidden">
                    <h2 class="text-xl font-bold text-[#003366] mb-6 uppercase">VEHICLE INFORMATION</h2>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label for="vehicleType" class="block text-sm font-medium text-gray-700 mb-2">Vehicle Type: <span class="text-red-600">*</span></label>
                            <select id="vehicleType" name="vehicleType" onchange="toggleOtherVehicleField()"
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                                <option value="" selected disabled>-- Select vehicle type --</option>
                                <option value="sedan">Sedan</option>
                                <option value="motorcycle">Motorcycles</option>
                                <option value="ebike">E-bike/E-trikes</option>
                                <option value="pickup">Pick-up Truck</option>
                                <option value="suv">SUV</option>
                                <option value="van">Van</option>
                                <option value="jeep">Jeep</option>
                                <option value="other">Other (please specify)</option>
                            </select>
                            <div class="error-message hidden" id="vehicleType-error">Please select vehicle type</div>
                        </div>
                        <div id="otherVehicleContainer" class="hidden">
                            <label for="otherVehicleType" class="block text-sm font-medium text-gray-700 mb-2">Please specify vehicle type: <span class="text-red-600">*</span></label>
                            <input type="text" id="otherVehicleType" name="otherVehicleType"
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="otherVehicleType-error">Please specify vehicle type</div>
                        </div>
                        <div>
                            <label for="plateNumber" class="block text-sm font-medium text-gray-700 mb-2">Plate Number: <span class="text-red-600">*</span></label>
                            <input type="text" id="plateNumber" name="plateNumber"
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="plateNumber-error">Please enter plate number</div>
                        </div>
                        <div>
                            <label for="yearModel" class="block text-sm font-medium text-gray-700 mb-2">Year Model/Car Make: <span class="text-red-600">*</span></label>
                            <input type="text" id="yearModel" name="yearModel"
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="yearModel-error">Please enter year model/car make</div>
                        </div>
                        <div>
                            <label for="vehicleColor" class="block text-sm font-medium text-gray-700 mb-2">Vehicle Color: <span class="text-red-600">*</span></label>
                            <input type="text" id="vehicleColor" name="vehicleColor"
                                class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-[#003366] focus:border-[#003366]">
                            <div class="error-message hidden" id="vehicleColor-error">Please enter vehicle color</div>
                        </div>
                    </div>
                </div>
                
                <!-- Email Notification Section -->
                <div id="emailNotificationSection" class="mb-8">
                    <h2 class="text-xl font-bold text-[#003366] mb-6 uppercase">APPLICATION SUMMARY</h2>
                    
                    <div class="p-4 bg-blue-50 border border-blue-200 rounded-md">
                        <div class="flex items-start">
                            <div class="flex-shrink-0 mt-0.5">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-blue-600" viewBox="0 0 20 20" fill="currentColor">
                                    <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd" />
                                </svg>
                            </div>
                            <div class="ml-3">
                                <p class="text-sm text-blue-700">
                                    A summary of your application will be sent to <strong>oas@gbox.adnu.edu.ph</strong> upon submission.
                                </p>
                            </div>
                        </div>
                    </div>
                </div>
                
                <!-- Submit Button -->
                <div class="mt-10 flex justify-center">
                    <button type="submit" class="btn-submit px-8 py-3 text-white font-bold rounded-md text-lg uppercase tracking-wider">
                        Submit Application
                    </button>
                </div>
                
                <!-- Success Message (Hidden by default) -->
                <div id="successMessage" class="hidden mt-6 p-4 bg-green-100 border border-green-400 text-green-700 rounded-md text-center">
                    <p class="font-medium">Your gate pass application has been submitted successfully!</p>
                    <p class="mt-2">An application summary has been sent to oas@gbox.adnu.edu.ph</p>
                    <div class="mt-4">
                        <button onclick="printSummary()" class="px-4 py-2 bg-[#003366] text-white rounded-md hover:bg-[#002244] flex items-center mx-auto">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" viewBox="0 0 20 20" fill="currentColor">
                                <path fill-rule="evenodd" d="M5 4v3H4a2 2 0 00-2 2v3a2 2 0 002 2h1v2a2 2 0 002 2h6a2 2 0 002-2v-2h1a2 2 0 002-2V9a2 2 0 00-2-2h-1V4a2 2 0 00-2-2H7a2 2 0 00-2 2zm8 0H7v3h6V4zm0 8H7v4h6v-4z" clip-rule="evenodd" />
                            </svg>
                            Print Summary
                        </button>
                    </div>
                </div>
            </form>
        </div>
    </div>
    
    <!-- Application Summary Modal (Hidden by default) -->
    <div id="summaryModal" class="modal hidden">
        <div class="modal-content p-6">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-xl font-bold text-[#003366]">APPLICATION SUMMARY</h2>
                <button onclick="closeSummaryModal()" class="text-gray-500 hover:text-gray-700 no-print">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                </button>
            </div>
            
            <div class="university-blue rounded-lg py-3 px-4 mb-4">
                <h3 class="text-lg font-bold text-white">ATENEO DE NAGA UNIVERSITY</h3>
                <p class="university-gold text-sm font-semibold">Gate Pass Application Summary</p>
            </div>
            
            <div id="summaryContent" class="application-summary">
                <!-- Summary content will be populated by JavaScript -->
            </div>
            
            <div class="mt-6 flex justify-end no-print">
                <button onclick="closeSummaryModal()" class="px-4 py-2 bg-gray-200 text-gray-800 rounded-md mr-2 hover:bg-gray-300">
                    Close
                </button>
                <button onclick="printSummary()" class="px-4 py-2 bg-gray-200 text-gray-800 rounded-md mr-2 hover:bg-gray-300 flex items-center">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M5 4v3H4a2 2 0 00-2 2v3a2 2 0 002 2h1v2a2 2 0 002 2h6a2 2 0 002-2v-2h1a2 2 0 002-2V9a2 2 0 00-2-2h-1V4a2 2 0 00-2-2H7a2 2 0 00-2 2zm8 0H7v3h6V4zm0 8H7v4h6v-4z" clip-rule="evenodd" />
                    </svg>
                    Print
                </button>
                <button onclick="sendApplicationSummary()" class="px-4 py-2 bg-[#003366] text-white rounded-md hover:bg-[#002244]">
                    Send Summary
                </button>
            </div>
        </div>
    </div>
    
    <!-- Printable Summary (Hidden by default) -->
    <div id="printSummary" class="hidden">
        <div class="p-8">
            <div style="background-color: #003366;" class="rounded-lg py-3 px-4 mb-4 text-center">
                <h3 class="text-lg font-bold text-white">ATENEO DE NAGA UNIVERSITY</h3>
                <p style="color: #FFD700;" class="text-sm font-semibold">Gate Pass Application Summary</p>
            </div>
            
            <div id="printSummaryContent" class="mt-4">
                <!-- Print summary content will be populated by JavaScript -->
            </div>
        </div>
    </div>

    <script>
        // Database simulation for ID numbers that have already been used
        // In a real application, this would be stored in a server database
        const usedIdNumbers = new Set();
        
        // Restricted vehicle types that require ID number check
        const restrictedVehicleTypes = ['sedan', 'pickup', 'suv', 'van', 'jeep', 'other'];
        
        // Show relevant sections when the page loads
        document.addEventListener('DOMContentLoaded', function() {
            // Add input validation listeners
            addInputValidationListeners();
        });
        
        function addInputValidationListeners() {
            // Add blur event listeners to all required inputs
            const requiredInputs = document.querySelectorAll('input[required], select[required]');
            requiredInputs.forEach(input => {
                input.addEventListener('blur', function() {
                    validateField(this);
                });
                
                input.addEventListener('input', function() {
                    // Remove error styling when user starts typing
                    if (this.value.trim() !== '') {
                        this.classList.remove('input-error');
                        const errorElement = document.getElementById(`${this.id}-error`);
                        if (errorElement) {
                            errorElement.classList.add('hidden');
                        }
                        
                        // Also hide duplicate error if applicable
                        const duplicateErrorElement = document.getElementById(`${this.id}-duplicate-error`);
                        if (duplicateErrorElement) {
                            duplicateErrorElement.classList.add('hidden');
                        }
                        
                        // Hide the global duplicate ID message
                        document.getElementById('duplicateIdMessage').classList.add('hidden');
                    }
                });
            });
            
            // Add email validation listeners
            const emailInputs = document.querySelectorAll('input[type="email"]');
            emailInputs.forEach(input => {
                input.addEventListener('blur', function() {
                    validateEmail(this);
                });
            });
            
            // Add vehicle type change listener
            const vehicleTypeSelect = document.getElementById('vehicleType');
            if (vehicleTypeSelect) {
                vehicleTypeSelect.addEventListener('change', function() {
                    // If vehicle type changes, recheck ID numbers
                    const studentIdField = document.getElementById('studentId');
                    const employeeIdField = document.getElementById('employeeId');
                    
                    if (studentIdField && studentIdField.value) {
                        checkDuplicateId(studentIdField);
                    }
                    
                    if (employeeIdField && employeeIdField.value) {
                        checkDuplicateId(employeeIdField);
                    }
                });
            }
        }
        
        function checkDuplicateId(field) {
            const idValue = field.value.trim();
            if (!idValue) return true;
            
            const vehicleType = document.getElementById('vehicleType').value;
            const duplicateErrorElement = document.getElementById(`${field.id}-duplicate-error`);
            const globalDuplicateMessage = document.getElementById('duplicateIdMessage');
            
            // Only check for duplicates if the vehicle type is restricted
            if (restrictedVehicleTypes.includes(vehicleType)) {
                if (usedIdNumbers.has(idValue)) {
                    // Show error message
                    field.classList.add('input-error');
                    if (duplicateErrorElement) {
                        duplicateErrorElement.classList.remove('hidden');
                    }
                    globalDuplicateMessage.classList.remove('hidden');
                    globalDuplicateMessage.scrollIntoView({ behavior: 'smooth' });
                    return false;
                } else {
                    // Hide error message
                    if (duplicateErrorElement) {
                        duplicateErrorElement.classList.add('hidden');
                    }
                    globalDuplicateMessage.classList.add('hidden');
                    return true;
                }
            }
            
            // If vehicle type is not restricted, always return true
            if (duplicateErrorElement) {
                duplicateErrorElement.classList.add('hidden');
            }
            globalDuplicateMessage.classList.add('hidden');
            return true;
        }
        
        function validateEmail(field) {
            const errorElement = document.getElementById(`${field.id}-error`);
            const verifiedBadge = document.getElementById(`${field.id}-verified`);
            
            if (!errorElement || !verifiedBadge) return true;
            
            const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            const isValid = emailRegex.test(field.value);
            
            if (field.hasAttribute('required') && field.value.trim() === '') {
                field.classList.add('input-error');
                errorElement.classList.remove('hidden');
                verifiedBadge.classList.remove('active');
                return false;
            } else if (field.value.trim() !== '' && !isValid) {
                field.classList.add('input-error');
                errorElement.classList.remove('hidden');
                errorElement.textContent = 'Please enter a valid email address';
                verifiedBadge.classList.remove('active');
                return false;
            } else if (field.value.trim() !== '' && isValid) {
                field.classList.remove('input-error');
                errorElement.classList.add('hidden');
                verifiedBadge.classList.add('active');
                return true;
            } else {
                field.classList.remove('input-error');
                errorElement.classList.add('hidden');
                verifiedBadge.classList.remove('active');
                return true;
            }
        }
        
        function validateField(field) {
            // Special handling for email fields
            if (field.type === 'email') {
                return validateEmail(field);
            }
            
            // Special handling for ID fields
            if (field.id === 'studentId' || field.id === 'employeeId') {
                const basicValidation = field.value.trim() !== '';
                const duplicateCheck = checkDuplicateId(field);
                
                const errorElement = document.getElementById(`${field.id}-error`);
                if (!basicValidation) {
                    field.classList.add('input-error');
                    if (errorElement) errorElement.classList.remove('hidden');
                } else {
                    if (errorElement) errorElement.classList.add('hidden');
                }
                
                return basicValidation && duplicateCheck;
            }
            
            const errorElement = document.getElementById(`${field.id}-error`);
            if (!errorElement) return true;
            
            let isValid = true;
            
            if (field.hasAttribute('required') && field.value.trim() === '') {
                field.classList.add('input-error');
                errorElement.classList.remove('hidden');
                isValid = false;
            } else {
                field.classList.remove('input-error');
                errorElement.classList.add('hidden');
            }
            
            return isValid;
        }
        
        function toggleAffiliationSections() {
            const affiliation = document.getElementById('affiliation').value;
            const studentSection = document.getElementById('studentSection');
            const employeeSection = document.getElementById('employeeSection');
            const concessionaireSection = document.getElementById('concessionaireSection');
            const vehicleSection = document.getElementById('vehicleSection');
            
            // Hide all sections first
            studentSection.classList.add('hidden');
            employeeSection.classList.add('hidden');
            concessionaireSection.classList.add('hidden');
            vehicleSection.classList.add('hidden');
            
            // Reset required attributes
            setRequiredFields('studentSection', false);
            setRequiredFields('employeeSection', false);
            setRequiredFields('concessionaireSection', false);
            setRequiredFields('vehicleSection', false);
            
            // Show relevant sections based on affiliation
            if (affiliation === 'student') {
                studentSection.classList.remove('hidden');
                vehicleSection.classList.remove('hidden');
                setRequiredFields('studentSection', true);
                setRequiredFields('vehicleSection', true);
            } else if (affiliation === 'employee') {
                employeeSection.classList.remove('hidden');
                vehicleSection.classList.remove('hidden');
                setRequiredFields('employeeSection', true);
                setRequiredFields('vehicleSection', true);
            } else if (affiliation === 'concessionaire') {
                concessionaireSection.classList.remove('hidden');
                vehicleSection.classList.remove('hidden');
                setRequiredFields('concessionaireSection', true);
                setRequiredFields('vehicleSection', true);
            }
            
            // Add validation listeners to newly visible fields
            addInputValidationListeners();
        }
        
        function setRequiredFields(sectionId, isRequired) {
            const section = document.getElementById(sectionId);
            const inputs = section.querySelectorAll('input, select');
            
            inputs.forEach(input => {
                if (isRequired) {
                    input.setAttribute('required', 'required');
                } else {
                    input.removeAttribute('required');
                    // Reset any error styling
                    input.classList.remove('input-error');
                    const errorElement = document.getElementById(`${input.id}-error`);
                    if (errorElement) {
                        errorElement.classList.add('hidden');
                    }
                    // Reset verified badge for email fields
                    if (input.type === 'email') {
                        const verifiedBadge = document.getElementById(`${input.id}-verified`);
                        if (verifiedBadge) {
                            verifiedBadge.classList.remove('active');
                        }
                    }
                    // Reset duplicate error for ID fields
                    if (input.id === 'studentId' || input.id === 'employeeId') {
                        const duplicateErrorElement = document.getElementById(`${input.id}-duplicate-error`);
                        if (duplicateErrorElement) {
                            duplicateErrorElement.classList.add('hidden');
                        }
                    }
                }
            });
        }
        
        function toggleOtherVehicleField() {
            const vehicleType = document.getElementById('vehicleType').value;
            const otherVehicleContainer = document.getElementById('otherVehicleContainer');
            const otherVehicleInput = document.getElementById('otherVehicleType');
            
            if (vehicleType === 'other') {
                otherVehicleContainer.classList.remove('hidden');
                otherVehicleInput.setAttribute('required', 'required');
            } else {
                otherVehicleContainer.classList.add('hidden');
                otherVehicleInput.removeAttribute('required');
                // Reset any error styling
                otherVehicleInput.classList.remove('input-error');
                const errorElement = document.getElementById('otherVehicleType-error');
                if (errorElement) {
                    errorElement.classList.add('hidden');
                }
            }
            
            // Recheck ID numbers when vehicle type changes
            const studentIdField = document.getElementById('studentId');
            const employeeIdField = document.getElementById('employeeId');
            
            if (studentIdField && studentIdField.value) {
                checkDuplicateId(studentIdField);
            }
            
            if (employeeIdField && employeeIdField.value) {
                checkDuplicateId(employeeIdField);
            }
        }
        
        function validateForm() {
            let isValid = true;
            const formErrorMessage = document.getElementById('formErrorMessage');
            const duplicateIdMessage = document.getElementById('duplicateIdMessage');
            
            // Reset section error styling
            const sections = document.querySelectorAll('form > div');
            sections.forEach(section => {
                section.classList.remove('section-error');
            });
            
            // Hide error messages
            formErrorMessage.classList.add('hidden');
            duplicateIdMessage.classList.add('hidden');
            
            // Validate all visible required fields
            const visibleRequiredFields = document.querySelectorAll('div:not(.hidden) input[required], div:not(.hidden) select[required]');
            visibleRequiredFields.forEach(field => {
                if (!validateField(field)) {
                    isValid = false;
                    // Find the parent section and add error styling
                    let currentElement = field;
                    while (currentElement && !currentElement.id.includes('Section')) {
                        currentElement = currentElement.parentElement;
                    }
                    if (currentElement) {
                        currentElement.classList.add('section-error');
                    }
                }
            });
            
            // Check for duplicate IDs
            const affiliation = document.getElementById('affiliation').value;
            const vehicleType = document.getElementById('vehicleType').value;
            
            if (restrictedVehicleTypes.includes(vehicleType)) {
                if (affiliation === 'student') {
                    const studentIdField = document.getElementById('studentId');
                    if (studentIdField && !checkDuplicateId(studentIdField)) {
                        isValid = false;
                    }
                } else if (affiliation === 'employee') {
                    const employeeIdField = document.getElementById('employeeId');
                    if (employeeIdField && !checkDuplicateId(employeeIdField)) {
                        isValid = false;
                    }
                }
            }
            
            // Show form error message if needed
            if (!isValid && !duplicateIdMessage.classList.contains('hidden')) {
                // If duplicate ID error is showing, scroll to it
                duplicateIdMessage.scrollIntoView({ behavior: 'smooth' });
            } else if (!isValid) {
                // Otherwise show general form error
                formErrorMessage.classList.remove('hidden');
                formErrorMessage.scrollIntoView({ behavior: 'smooth' });
            }
            
            return isValid;
        }
        
        function getFormData() {
            const formData = {};
            
            // Get applicant information
            formData.applicantName = document.getElementById('applicantName').value;
            formData.driversLicense = document.getElementById('driversLicense').value;
            formData.applicantContact = document.getElementById('applicantContact').value;
            formData.applicantEmail = document.getElementById('applicantEmail').value;
            formData.address = document.getElementById('address').value;
            
            // Get affiliation
            const affiliationSelect = document.getElementById('affiliation');
            formData.affiliation = affiliationSelect.value;
            formData.affiliationText = affiliationSelect.options[affiliationSelect.selectedIndex].text;
            
            // Get student information if applicable
            if (formData.affiliation === 'student') {
                formData.studentName = document.getElementById('studentName').value;
                formData.studentId = document.getElementById('studentId').value;
                formData.studentContact = document.getElementById('studentContact').value;
                formData.studentEmail = document.getElementById('studentEmail').value;
                formData.yearLevel = document.getElementById('yearLevel').value;
                
                const courseSelect = document.getElementById('course');
                formData.course = courseSelect.value;
                formData.courseText = courseSelect.options[courseSelect.selectedIndex].text;
            }
            
            // Get employee information if applicable
            if (formData.affiliation === 'employee') {
                formData.employeeName = document.getElementById('employeeName').value;
                formData.employeeId = document.getElementById('employeeId').value;
                formData.employeeContact = document.getElementById('employeeContact').value;
                formData.employeeEmail = document.getElementById('employeeEmail').value;
                formData.department = document.getElementById('department').value;
                formData.position = document.getElementById('position').value;
            }
            
            // Get concessionaire information if applicable
            if (formData.affiliation === 'concessionaire') {
                formData.companyName = document.getElementById('companyName').value;
                formData.businessType = document.getElementById('businessType').value;
                formData.contactNumber = document.getElementById('contactNumber').value;
            }
            
            // Get vehicle information
            if (!document.getElementById('vehicleSection').classList.contains('hidden')) {
                const vehicleTypeSelect = document.getElementById('vehicleType');
                formData.vehicleType = vehicleTypeSelect.value;
                formData.vehicleTypeText = vehicleTypeSelect.options[vehicleTypeSelect.selectedIndex].text;
                
                if (formData.vehicleType === 'other') {
                    formData.otherVehicleType = document.getElementById('otherVehicleType').value;
                }
                
                formData.plateNumber = document.getElementById('plateNumber').value;
                formData.yearModel = document.getElementById('yearModel').value;
                formData.vehicleColor = document.getElementById('vehicleColor').value;
            }
            
            // Add application date
            formData.applicationDate = new Date().toLocaleDateString('en-US', {
                year: 'numeric',
                month: 'long',
                day: 'numeric'
            });
            
            // Add application ID (random for demo)
            formData.applicationId = 'GP-' + Math.floor(100000 + Math.random() * 900000);
            
            return formData;
        }
        
        function generateSummaryHTML(formData) {
            let html = `
                <div class="mb-4">
                    <div class="summary-item">
                        <div class="summary-label">Application ID:</div>
                        <div class="summary-value font-bold">${formData.applicationId}</div>
                    </div>
                    <div class="summary-item">
                        <div class="summary-label">Application Date:</div>
                        <div class="summary-value">${formData.applicationDate}</div>
                    </div>
                </div>
                
                <h4 class="font-bold text-[#003366] mb-2">APPLICANT'S INFORMATION</h4>
                <div class="mb-4">
                    <div class="summary-item">
                        <div class="summary-label">Full Name:</div>
                        <div class="summary-value">${formData.applicantName}</div>
                    </div>
                    <div class="summary-item">
                        <div class="summary-label">Driver's License:</div>
                        <div class="summary-value">${formData.driversLicense}</div>
                    </div>
                    <div class="summary-item">
                        <div class="summary-label">Contact Number:</div>
                        <div class="summary-value">${formData.applicantContact}</div>
                    </div>
                    <div class="summary-item">
                        <div class="summary-label">Email Address:</div>
                        <div class="summary-value">${formData.applicantEmail}</div>
                    </div>
                    <div class="summary-item">
                        <div class="summary-label">Address:</div>
                        <div class="summary-value">${formData.address}</div>
                    </div>
                </div>
                
                <h4 class="font-bold text-[#003366] mb-2">AFFILIATION</h4>
                <div class="mb-4">
                    <div class="summary-item">
                        <div class="summary-label">Affiliation Type:</div>
                        <div class="summary-value">${formData.affiliationText}</div>
                    </div>
                </div>
            `;
            
            // Add student information if applicable
            if (formData.affiliation === 'student') {
                html += `
                    <h4 class="font-bold text-[#003366] mb-2">STUDENT'S INFORMATION</h4>
                    <div class="mb-4">
                        <div class="summary-item">
                            <div class="summary-label">Student's Name:</div>
                            <div class="summary-value">${formData.studentName}</div>
                        </div>
                        <div class="summary-item">
                            <div class="summary-label">Student ID:</div>
                            <div class="summary-value">${formData.studentId}</div>
                        </div>
                        <div class="summary-item">
                            <div class="summary-label">Contact Number:</div>
                            <div class="summary-value">${formData.studentContact}</div>
                        </div>
                        <div class="summary-item">
                            <div class="summary-label">Email Address:</div>
                            <div class="summary-value">${formData.studentEmail}</div>
                        </div>
                        <div class="summary-item">
                            <div class="summary-label">Year/Level:</div>
                            <div class="summary-value">${formData.yearLevel}</div>
                        </div>
                        <div class="summary-item">
                            <div class="summary-label">Academic Program:</div>
                            <div class="summary-value">${formData.courseText}</div>
                        </div>
                    </div>
                `;
            }
            
            // Add employee information if applicable
            if (formData.affiliation === 'employee') {
                html += `
                    <h4 class="font-bold text-[#003366] mb-2">EMPLOYEE'S INFORMATION</h4>
                    <div class="mb-4">
                        <div class="summary-item">
                            <div class="summary-label">Employee's Name:</div>
                            <div class="summary-value">${formData.employeeName}</div>
                        </div>
                        <div class="summary-item">
                            <div class="summary-label">Employee ID:</div>
                            <div class="summary-value">${formData.employeeId}</div>
                        </div>
                        <div class="summary-item">
                            <div class="summary-label">Contact Number:</div>
                            <div class="summary-value">${formData.employeeContact}</div>
                        </div>
                        <div class="summary-item">
                            <div class="summary-label">Email Address:</div>
                            <div class="summary-value">${formData.employeeEmail}</div>
                        </div>
                        <div class="summary-item">
                            <div class="summary-label">Department/Office:</div>
                            <div class="summary-value">${formData.department}</div>
                        </div>
                        <div class="summary-item">
                            <div class="summary-label">Position/Designation:</div>
                            <div class="summary-value">${formData.position}</div>
                        </div>
                    </div>
                `;
            }
            
            // Add concessionaire information if applicable
            if (formData.affiliation === 'concessionaire') {
                html += `
                    <h4 class="font-bold text-[#003366] mb-2">CONCESSIONAIRE/DELIVERY INFORMATION</h4>
                    <div class="mb-4">
                        <div class="summary-item">
                            <div class="summary-label">Company/Business Name:</div>
                            <div class="summary-value">${formData.companyName}</div>
                        </div>
                        <div class="summary-item">
                            <div class="summary-label">Type of Business/Service:</div>
                            <div class="summary-value">${formData.businessType}</div>
                        </div>
                        <div class="summary-item">
                            <div class="summary-label">Contact Number:</div>
                            <div class="summary-value">${formData.contactNumber}</div>
                        </div>
                    </div>
                `;
            }
            
            // Add vehicle information
            if (formData.vehicleType) {
                html += `
                    <h4 class="font-bold text-[#003366] mb-2">VEHICLE INFORMATION</h4>
                    <div class="mb-4">
                        <div class="summary-item">
                            <div class="summary-label">Vehicle Type:</div>
                            <div class="summary-value">${formData.vehicleType === 'other' ? formData.otherVehicleType : formData.vehicleTypeText}</div>
                        </div>
                        <div class="summary-item">
                            <div class="summary-label">Plate Number:</div>
                            <div class="summary-value">${formData.plateNumber}</div>
                        </div>
                        <div class="summary-item">
                            <div class="summary-label">Year Model/Car Make:</div>
                            <div class="summary-value">${formData.yearModel}</div>
                        </div>
                        <div class="summary-item">
                            <div class="summary-label">Vehicle Color:</div>
                            <div class="summary-value">${formData.vehicleColor}</div>
                        </div>
                    </div>
                `;
            }
            
            // Add payment information
            let paymentAmount = "P 230.00";
            if (formData.affiliation === 'concessionaire') {
                paymentAmount = "P 600.00";
            }
            
            html += `
                <h4 class="font-bold text-[#003366] mb-2">PAYMENT INFORMATION</h4>
                <div class="mb-4">
                    <div class="summary-item">
                        <div class="summary-label">Amount Due:</div>
                        <div class="summary-value font-bold">${paymentAmount}</div>
                    </div>
                    <div class="summary-item">
                        <div class="summary-label">Payment Status:</div>
                        <div class="summary-value text-yellow-600 font-medium">Pending</div>
                    </div>
                </div>
                
                <div class="mt-4 pt-4 border-t border-gray-200 text-sm text-gray-600">
                    <p>Please proceed to the Security Office with this application summary to complete your gate pass application process.</p>
                </div>
            `;
            
            return html;
        }
        
        function showSummaryModal() {
            const formData = getFormData();
            const summaryHTML = generateSummaryHTML(formData);
            
            document.getElementById('summaryContent').innerHTML = summaryHTML;
            document.getElementById('printSummaryContent').innerHTML = summaryHTML;
            document.getElementById('summaryModal').classList.remove('hidden');
            
            // Prevent scrolling of the background
            document.body.style.overflow = 'hidden';
        }
        
        function closeSummaryModal() {
            document.getElementById('summaryModal').classList.add('hidden');
            
            // Re-enable scrolling
            document.body.style.overflow = 'auto';
        }
        
        function printSummary() {
            // Update the print summary content
            const formData = getFormData();
            const summaryHTML = generateSummaryHTML(formData);
            document.getElementById('printSummaryContent').innerHTML = summaryHTML;
            
            // Print the summary
            window.print();
        }
        
        
function sendApplicationSummary() {
    const formData = getFormData();

    fetch("https://script.google.com/macros/s/https://script.google.com/a/macros/gbox.adnu.edu.ph/s/AKfycbysgPeYUXQPFxSWBtd92vi0DdNh3SRAlQiUehoNqu8pE55j6j37QzEAtawiZK5l8ez-w/exec", {
        method: "POST",
        body: JSON.stringify(formData),
        headers: {
            "Content-Type": "application/json"
        }
    })
    .then(response => response.json())
    .then(data => {
        if (data.status === "success") {
            const affiliation = document.getElementById('affiliation').value;
            const vehicleType = document.getElementById('vehicleType').value;

            if (restrictedVehicleTypes.includes(vehicleType)) {
                if (affiliation === 'student') {
                    const studentId = document.getElementById('studentId').value;
                    if (studentId) usedIdNumbers.add(studentId);
                } else if (affiliation === 'employee') {
                    const employeeId = document.getElementById('employeeId').value;
                    if (employeeId) usedIdNumbers.add(employeeId);
                }
            }

            closeSummaryModal();
            document.getElementById('successMessage').classList.remove('hidden');
            document.getElementById('successMessage').scrollIntoView({ behavior: 'smooth' });
            printSummary();
        } else {
            alert("Submission failed. Please try again later.");
        }
    })
    .catch(error => {
        console.error("Error:", error);
        alert("An error occurred. Please try again.");
    });
}

                } else if (affiliation === 'employee') {
                    const employeeId = document.getElementById('employeeId').value;
                    if (employeeId) {
                        usedIdNumbers.add(employeeId);
                    }
                }
            }
            
            // Close the modal
            closeSummaryModal();
            
            // Show success message
            document.getElementById('successMessage').classList.remove('hidden');
            document.getElementById('successMessage').scrollIntoView({ behavior: 'smooth' });
        }
        
        function submitForm(event) {
            event.preventDefault();
            
            // Validate the form
            if (!validateForm()) {
                return false;
            }
            
            // Show the summary modal
            showSummaryModal();
        }
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'947eed165052fec9',t:'MTc0ODYxNTM5Mi4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
