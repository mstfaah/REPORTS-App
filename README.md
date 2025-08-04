<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title data-key="appTitle">REPORTS</title>
    <!-- تحميل Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* الخط الافتراضي */
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f0f4f8; /* خلفية رمادية فاتحة */
            transition: background-color 0.5s ease; /* انتقال سلس للخلفية */
        }
        /* وضع الطوارئ */
        body.emergency-mode {
            background-color: #fee2e2; /* أحمر فاتح جداً للطوارئ */
        }
        body.emergency-mode .container {
            border: 2px solid #ef4444; /* حدود حمراء */
            box-shadow: 0 4px 20px rgba(239, 68, 68, 0.2); /* ظل أحمر */
        }
        body.emergency-mode .app-header .title,
        body.emergency-mode label,
        body.emergency-mode .input-field,
        body.emergency-mode .btn {
            color: #b91c1c; /* نص أحمر داكن */
        }
        body.emergency-mode .input-field {
            border-color: #ef4444; /* حدود حمراء */
        }
        body.emergency-mode .btn-primary {
            background-image: linear-gradient(to right, #ef4444 0%, #dc2626 50%, #ef4444 100%); /* تدرج أحمر */
        }
        body.emergency-mode .btn-secondary {
            background-color: #b91c1c; /* أحمر داكن */
        }
        body.emergency-mode .btn-secondary:hover {
            background-color: #991b1b; /* أحمر أغمق */
        }
        body.emergency-mode .favorite-site-tag {
            background-color: #fca5a5; /* أحمر فاتح */
            color: #b91c1c; /* أحمر داكن */
        }
        body.emergency-mode .favorite-site-tag:hover {
            background-color: #f87171; /* أحمر أغمق */
        }
        body.emergency-mode .message-box {
            background-color: #ef4444; /* أحمر لرسائل الطوارئ */
        }


        /* حاوية التطبيق الرئيسية */
        .container {
            max-width: 600px;
            margin: 2rem auto;
            padding: 1.5rem;
            background-color: #ffffff;
            border-radius: 1rem;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1); /* ظل خفيف */
            transition: all 0.5s ease; /* انتقال سلس للحدود والظل */
        }
        /* تنسيق تسميات الإدخال */
        .input-group label {
            font-weight: bold;
            margin-bottom: 0.5rem;
            display: block;
            color: #334155; /* نص أغمق للتسميات */
        }
        /* تنسيق حقول الإدخال والنصوص */
        .input-field {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid #cbd5e1; /* حدود رمادية فاتحة */
            border-radius: 0.5rem;
            font-size: 1rem;
            color: #475569; /* نص رمادي متوسط */
            transition: all 0.3s ease; /* انتقال سلس للحقول */
        }
        /* تنسيق الأزرار العامة */
        .btn {
            padding: 1rem 1.5rem;
            border-radius: 0.75rem;
            font-weight: bold;
            cursor: pointer;
            transition: background-color 0.3s ease; /* انتقال سلس عند التحويم */
            font-size: 1.125rem; /* خط أكبر للأزرار */
        }
        /* تنسيق الزر الأساسي (الإرسال) */
        .btn-primary {
            /* إضافة تدرج لوني وتأثير الانزلاق */
            background-image: linear-gradient(to right, #22c55e 0%, #16a34a 50%, #22c55e 100%);
            background-size: 200% auto; /* ضعف الحجم الأصلي للسماح بالانزلاق */
            color: white;
            transition: background-position 0.5s ease; /* انتقال سلس لموضع الخلفية */
        }
        .btn-primary:hover {
            background-position: -100% 0; /* تحريك الخلفية لليمين (لليسار في RTL) */
        }
        /* تنسيق الزر الثانوي (التقاط الصورة) */
        .btn-secondary {
            background-color: #64748b; /* رمادي للزر الثانوي */
            color: white;
        }
        .btn-secondary:hover {
            background-color: #475569; /* رمادي أغمق عند التحويم */
        }
        /* تنسيق بطاقات التقرير المعروضة */
        .report-card {
            background-color: #f8fafc; /* أزرق رمادي فاتح جداً لبطاقات التقرير */
            border: 1px solid #e2e8f0;
            border-radius: 0.75rem;
            padding: 1rem;
            margin-bottom: 1rem;
            box-shadow: 0 2px 6px rgba(0, 0, 0, 0.05); /* ظل خفيف */
        }
        /* تنسيق الصور داخل بطاقات التقرير */
        .report-card img {
            max-width: 100%;
            height: auto;
            border-radius: 0.5rem;
            margin-top: 0.75rem;
        }
        /* تنسيق صندوق الرسائل (للتأكيد/الخطأ) */
        .message-box {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: #22c55e; /* أخضر افتراضي للنجاح */
            color: white;
            padding: 1.5rem;
            border-radius: 1rem;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
            z-index: 1000; /* لضمان ظهوره فوق العناصر الأخرى */
            text-align: center;
            font-size: 1.25rem;
            display: none; /* مخفي افتراضياً */
        }
        /* تنسيق زر سلة المهملات للصورة */
        .delete-image-btn {
            background-color: #ef4444; /* أحمر */
            color: white;
            padding: 0.5rem;
            border-radius: 0.5rem;
            cursor: pointer;
            transition: background-color 0.3s ease;
            display: flex; /* لترتيب الأيقونة والنص */
            align-items: center;
            justify-content: center;
            font-size: 0.875rem; /* خط أصغر */
            line-height: 1; /* لضمان محاذاة الأيقونة والنص بشكل جيد */
            margin-top: 0.5rem; /* مسافة أعلى الزر */
            width: fit-content; /* حجم الزر حسب المحتوى */
        }
        .delete-image-btn:hover {
            background-color: #dc2626; /* أحمر أغمق عند التحويم */
        }
        .delete-image-btn svg {
            width: 1rem; /* حجم أيقونة سلة المهملات */
            height: 1rem;
            margin-left: 0.25rem; /* مسافة بين النص والأيقونة */
        }
        /* تنسيق رأس التطبيق مع الشعار والعنوان */
        .app-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 0.5rem; /* تقليل المسافة بعد العنوان الرئيسي */
            padding-bottom: 1rem;
            border-bottom: 1px solid #e2e8f0; /* خط فاصل */
            flex-wrap: wrap; /* للسماح بالعناصر بالانتقال إلى سطر جديد على الشاشات الصغيرة */
        }
        .app-header .logo { /* هذا النمط لم يعد مستخدمًا ولكن تم الاحتفاظ به في حالة إعادة إضافة الشعار */
            max-height: 60px; /* حجم الشعار */
            width: auto;
            border-radius: 0.5rem; /* حواف دائرية للشعار */
            order: 2; /* ترتيب الشعار ليكون على اليمين في التخطيط RTL */
            margin-right: 0;
            margin-left: auto; /* دفع الشعار إلى أقصى اليمين */
        }
        .app-header .title-container {
            flex-grow: 1; /* للسماح للحاوية بأخذ المساحة المتاحة */
            text-align: center; /* محاذاة العنوان والنص الفرعي في المنتصف */
            order: 1; /* ترتيب العنوان ليكون أولاً */
            width: 100%; /* لضمان أن يأخذ العنوان سطرًا كاملاً على الشاشات الصغيرة */
        }
        .app-header .title {
            font-size: 2.25rem; /* حجم خط أكبر للعنوان */
            font-weight: bold;
            color: #1a202c; /* لون داكن للعنوان */
            margin-bottom: 0.25rem; /* مسافة صغيرة بين العنوان والنص الفرعي */
        }
        .app-header .copyright-text {
            font-size: 0.75rem; /* حجم خط صغير جداً */
            color: #64748b; /* لون رمادي فاتح للنص */
            display: block; /* لضمان أن يكون النص في سطر خاص به */
            margin-top: 0.25rem; /* مسافة صغيرة أعلى النص */
        }

        /* تعديلات على الشاشات الصغيرة */
        @media (max-width: 640px) {
            .app-header {
                flex-direction: column; /* ترتيب عمودي على الشاشات الصغيرة */
                align-items: center; /* محاذاة العناصر في المنتصف */
                text-align: center;
            }
            .app-header .logo {
                order: 1; /* الشعار أولاً */
                margin-left: 0;
                margin-right: 0;
                margin-bottom: 1rem; /* مسافة تحت الشعار */
            }
            .app-header .title-container {
                order: 2; /* العنوان ثانياً */
                width: auto; /* السماح للحاوية بتحديد عرضها تلقائيًا */
            }
            .app-header .title {
                font-size: 2rem; /* تقليل حجم الخط على الشاشات الصغيرة */
            }
        }

        /* تنسيق المفضلة */
        .favorite-site-tag {
            background-color: #e0e7ff; /* لون خلفية خفيف */
            color: #4338ca; /* لون نص أزرق داكن */
            padding: 0.4rem 0.8rem;
            border-radius: 0.5rem;
            font-size: 0.9rem;
            cursor: pointer;
            transition: background-color 0.2s ease;
            white-space: nowrap; /* منع النص من الالتفاف */
        }
        .favorite-site-tag:hover {
            background-color: #c7d2fe; /* لون أغمق عند التحويم */
        }
        .favorite-sites-container {
            display: flex;
            flex-wrap: wrap; /* للسماح بالعناصر بالانتقال إلى سطر جديد */
            gap: 0.5rem; /* مسافة بين العناصر */
            margin-bottom: 1rem; /* مسافة تحت المفضلة */
        }
        /* Language selector styling */
        .language-selector {
            margin-left: 1rem; /* Space from logo/title */
            padding: 0.5rem;
            border-radius: 0.5rem;
            border: 1px solid #cbd5e1;
            background-color: #f8fafc;
            color: #334155;
            font-size: 0.9rem;
            cursor: pointer;
        }
        @media (max-width: 640px) {
            .language-selector {
                margin-top: 1rem; /* Space above selector on small screens */
                margin-left: 0;
            }
        }
        /* Enhanced select styling */
        .input-field.select-enhanced {
            appearance: none; /* Remove default browser arrow */
            background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 20 20' fill='currentColor'%3E%3Cpath fill-rule='evenodd' d='M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z' clip-rule='evenodd'/%3E%3C/svg%3E"); /* Custom SVG arrow */
            background-repeat: no-repeat;
            background-position: left 0.75rem center; /* Position arrow on the left for RTL */
            background-size: 1.5em 1.5em; /* Size of the arrow */
            padding-left: 2.5rem; /* Space for the arrow */
            padding-right: 0.75rem; /* Keep original right padding */
        }
        html[dir="ltr"] .input-field.select-enhanced {
            background-position: right 0.75rem center; /* Position arrow on the right for LTR */
            padding-right: 2.5rem; /* Space for the arrow */
            padding-left: 0.75rem; /* Keep original left padding */
        }
    </style>
</head>
<body class="p-4">
    <div class="container">
        <!-- رأس التطبيق مع الشعار والعنوان ومحدد اللغة -->
        <div class="app-header">
            <div class="title-container">
                <h1 class="title" data-key="appTitle">REPORTS</h1>
                <small class="copyright-text">MR.MSTFA</small>
            </div>
            <!-- محدد اللغة -->
            <select id="languageSelector" class="language-selector">
                <option value="ar">العربية</option>
                <option value="en">English</option>
            </select>
        </div>

        <!-- قسم معلومات البلاغ (التاريخ والوقت يدوياً) -->
        <div class="mb-6 p-4 bg-blue-50 rounded-lg shadow-sm">
            <div class="mb-4">
                <label for="faultType" class="text-lg font-semibold text-gray-700 mb-2 block" data-key="labelFaultType">
                    نوع العطل:
                </label>
                <select id="faultType" class="input-field select-enhanced"> <!-- Added select-enhanced class -->
                    <option value="" data-key="selectFaultTypePlaceholder">اختر نوع العطل</option>
                    <option value="بلاغ عن عطل في الإضاءة" data-key="faultTypeLighting">بلاغ عن عطل في الإضاءة</option>
                    <option value="بلاغ عن خلل في المكيف" data-key="faultTypeHVAC">بلاغ عن خلل في المكيف</option>
                    <option value="تنظيف وصيانة دورات المياه" data-key="faultTypeCleaning">تنظيف وصيانة دورات المياه</option>
                    <option value="طلب إصلاح أو استبدال كراسي" data-key="faultTypeChairs">طلب إصلاح أو استبدال كراسي</option>
                    <option value="أعمال زراعية وصيانة المسطحات الخضراء" data-key="faultTypeGardening">أعمال زراعية وصيانة المسطحات الخضراء</option>
                    <option value="مكافحة الحشرات ورش المبيدات" data-key="faultTypePestControl">مكافحة الحشرات ورش المبيدات</option>
                    <option value="emergency" data-key="faultTypeEmergency">بلاغ طارئ</option>
                    <option value="other" data-key="faultTypeOther">بلاغ آخر</option>
                </select>
            </div>
            <!-- مربع نص يظهر عند اختيار "بلاغ آخر" -->
            <div id="otherFaultTypeContainer" class="mb-4 hidden">
                <label for="otherFaultType" class="text-lg font-semibold text-gray-700 mb-2 block" data-key="labelOtherFaultType">
                    نوع العطل الآخر:
                </label>
                <input type="text" id="otherFaultType" class="input-field" placeholder="اكتب نوع العطل" data-key="placeholderOtherFaultType">
            </div>

            <div class="mb-4">
                <label for="reportDate" class="text-lg font-semibold text-gray-700 mb-2 block" data-key="labelDate">
                    التاريخ:
                </label>
                <input type="date" id="reportDate" class="input-field" required>
            </div>
            <div>
                <label for="reportTime" class="text-lg font-semibold text-gray-700 mb-2 block" data-key="labelTime">
                    الوقت:
                </label>
                <input type="time" id="reportTime" class="input-field" required>
            </div>
        </div>

        <!-- قسم التقاط الصورة -->
        <div class="mb-6">
            <label for="imageUpload" class="text-lg font-semibold text-gray-700 mb-2 block" data-key="labelCaptureImage">
                التقط صورة للعطل:
            </label>
            <!-- حقل إدخال الملف المخفي لتشغيل الكاميرا -->
            <input type="file" id="imageUpload" accept="image/*,video/*" capture="environment" class="hidden"> <!-- Added video/* to accept -->
            <!-- زر لتشغيل حقل إدخال الملف -->
            <button id="captureImageBtn" class="btn btn-secondary w-full flex items-center justify-center gap-2" data-key="btnCaptureImage">
                <!-- أيقونة الكاميرا (SVG) -->
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-6 h-6">
                    <path d="M4.5 4.5a3 3 0 0 0-3 3v9a3 3 0 0 0 3 3h15a3 3 0 0 0 3-3v-9a3 3 0 0 0-3-3H4.5ZM19.94 12.08a.75.75 0 0 0-.28-.51l-2.47-2.47a.75.75 0 0 0-.52-.22H14.25V7.5a.75.75 0 0 0-.75-.75h-3a.75.75 0 0 0-.75.75v1.34L7.02 9.1a.75.75 0 0 0-.51.28l-2.47 2.47a.75.75 0 0 0-.22.52V16.5a.75.75 0 0 0 .75.75h15a.75.75 0 0 0 .75-.75v-4.47a.75.75 0 0 0-.26-.5Z" />
                    <path fill-rule="evenodd" d="M12 7.5a.75.75 0 0 1 .75.75v1.5a.75.75 0 0 1-1.5 0v-1.5A.75.75 0 0 1 12 7.5ZM10.5 12a1.5 1.5 0 1 1 3 0 1.5 1.5 0 0 1-3 0Z" clip-rule="evenodd" />
                </svg>
                <span data-key="btnCaptureImageText">التقط صورة</span>
            </button>
            <!-- معاينة الصورة الملتقطة وزر الحذف -->
            <div id="imagePreviewContainer" class="mt-4 hidden relative">
                <img id="imagePreview" src="" alt="معاينة الصورة" class="w-full h-auto border border-gray-300 rounded-lg">
                <button id="deleteImageBtn" class="delete-image-btn absolute top-2 left-2" data-key="btnDeleteImage">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" class="w-4 h-4">
                        <path fill-rule="evenodd" d="M8.75 1A2.75 2.75 0 0 0 6 3.75v.443c-.795.077-1.584.176-2.365.298a.75.75 0 1 0 .23 1.482l.149-.022.841 10.518A2.75 2.75 0 0 0 7.594 19h4.812a2.75 2.75 0 0 0 2.742-2.53l.841-10.518.148.022a.75.75 0 0 0 .23-1.482A41.03 41.03 0 0 0 14 4.193V3.75A2.75 2.75 0 0 0 11.25 1h-2.5ZM10 4c.84 0 1.673.025 2.5.075V3.75c0-.69-.56-1.25-1.25-1.25h-2.5c-.69 0-1.25.56-1.25 1.25v.325C8.327 4.025 9.16 4 10 4ZM8.58 7.72a.75.75 0 0 0-1.5.06l.35 7.11a.75.75 0 0 0 1.5-.06l-.35-7.11Zm3.5 0a.75.75 0 0 0-1.5.06l-.35 7.11a.75.75 0 0 0 1.5-.06l.35-7.11Z" clip-rule="evenodd" />
                    </svg>
                </button>
            </div>
        </div>

        <!-- قسم اسم الموقع -->
        <div class="mb-6">
            <label for="siteName" class="text-lg font-semibold text-gray-700 mb-2 block" data-key="labelSiteName">
                اسم الموقع:
            </label>
            <!-- حاوية لعرض المواقع المفضلة -->
            <div id="favoriteSitesContainer" class="favorite-sites-container">
                <!-- سيتم إضافة المواقع المفضلة هنا بواسطة JavaScript -->
            </div>
            <input type="text" id="siteName" class="input-field" placeholder="أدخل اسم الموقع" required data-key="placeholderSiteName">
        </div>

        <!-- قسم وصف العطل -->
        <div class="mb-6">
            <label for="faultDescription" class="text-lg font-semibold text-gray-700 mb-2 block" data-key="labelFaultDescription">
                وصف العطل:
            </label>
            <textarea id="faultDescription" rows="4" class="input-field placeholder-gray-400" placeholder="اكتب وصفًا موجزًا للعطل هنا..." data-key="placeholderFaultDescription"></textarea>
        </div>

        <!-- مربع الملاحظات الجديد -->
        <div class="mb-6">
            <label for="notes" class="text-lg font-semibold text-gray-700 mb-2 block" data-ke
