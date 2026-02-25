<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-auth-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-database-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-storage-compat.js"></script>

    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام إدارة تقارير المبيعات - Hyma Plastic</title>
    <script src="https://cdn.tailwindcss.com/3.4.16"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.min.js"></script>
    <script>tailwind.config={theme:{extend:{colors:{primary:'#198a11',secondary:'#f59e0b'},borderRadius:{'none':'0px','sm':'4px',DEFAULT:'8px','md':'12px','lg':'16px','xl':'20px','2xl':'24px','3xl':'32px','full':'9999px','button':'8px'}}}}</script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Pacifico&display=swap" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/remixicon/4.6.0/remixicon.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;700&display=swap');
        body {
            font-family: 'Tajawal', sans-serif;
        }
        input::-webkit-outer-spin-button,
        input::-webkit-inner-spin-button {
            -webkit-appearance: none;
            margin: 0;
        }
        .add-btn-floating {
            animation: pulse 2s infinite;
        }
        @keyframes pulse {
            0%, 100% {
                box-shadow: 0 0 0 0 rgba(25, 138, 17, 0.7);
            }
            50% {
                box-shadow: 0 0 0 10px rgba(25, 138, 17, 0);
            }
        }
    </style>
</head>
<body class="bg-gray-50 min-h-screen">

    <!-- ===== صفحة تسجيل الدخول ===== -->
    <div id="login-page" class="min-h-screen flex flex-col items-center justify-center px-4 py-12">
        <div class="w-full max-w-md bg-white rounded-lg shadow-lg p-8">
            <div class="text-center mb-8">
                <h1 class="font-['avenir'] text-primary text-4xl">Hyma Plastic</h1>
                <p class="text-gray-600 mt-2">نظام إدارة المبيعات</p>
            </div>
            
            <form id="login-form" class="space-y-6">
                <div>
                    <label for="username" class="block text-sm font-medium text-gray-700 mb-1">اسم المستخدم</label>
                    <input type="text" id="username" class="block w-full px-4 py-3 border border-gray-300 bg-gray-50 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" placeholder="أدخل اسم المستخدم" required>
                </div>
                
                <div>
                    <label for="password" class="block text-sm font-medium text-gray-700 mb-1">كلمة المرور</label>
                    <input type="password" id="password" class="block w-full px-4 py-3 border border-gray-300 bg-gray-50 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" placeholder="أدخل كلمة المرور" required>
                </div>
                
                <div>
                    <button type="submit" class="w-full bg-primary text-white py-3 rounded-lg hover:bg-primary/90 transition duration-200 font-medium">تسجيل الدخول</button>
                </div>
            </form>
            
            <div class="mt-4 text-center">
                <a href="#" id="forgot-password-link" class="text-primary hover:text-primary/80 text-sm">نسيت كلمة المرور؟</a>
            </div>
            
            <div class="mt-6 text-center">
                <p class="text-gray-600">ليس لديك حساب؟ <a href="#" id="register-link" class="text-primary hover:text-primary/80 font-medium">إنشاء حساب جديد</a></p>
            </div>

            <div class="mt-6 p-3 bg-blue-50 rounded-lg">
                <p class="text-xs text-gray-600"><strong>بيانات تجريبية:</strong></p>
                <p class="text-xs text-gray-600">اسم المستخدم: user / كلمة المرور: 123</p>
            </div>
        </div>
    </div>

    <!-- ===== صفحة التسجيل ===== -->
    <div id="register-page" class="min-h-screen flex flex-col items-center justify-center px-4 py-12 hidden">
        <div class="w-full max-w-md bg-white rounded-lg shadow-lg p-8">
            <div class="text-center mb-8">
                <h1 class="font-['avenir'] text-primary text-3xl">Hyma Plastic</h1>
                <p class="text-gray-600 mt-2">إنشاء حساب جديد</p>
            </div>
            
            <form id="register-form" class="space-y-4">
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">الاسم الكامل</label>
                    <input type="text" id="fullname" class="block w-full px-4 py-3 border border-gray-300 bg-gray-50 rounded-lg focus:ring-2 focus:ring-primary" required>
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">البريد الإلكتروني</label>
                    <input type="email" id="email" class="block w-full px-4 py-3 border border-gray-300 bg-gray-50 rounded-lg focus:ring-2 focus:ring-primary" required>
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">رقم الهاتف</label>
                    <input type="tel" id="phone" class="block w-full px-4 py-3 border border-gray-300 bg-gray-50 rounded-lg focus:ring-2 focus:ring-primary" required>
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">كلمة المرور</label>
                    <input type="password" id="new-password" class="block w-full px-4 py-3 border border-gray-300 bg-gray-50 rounded-lg focus:ring-2 focus:ring-primary" required>
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">تأكيد كلمة المرور</label>
                    <input type="password" id="confirm-password" class="block w-full px-4 py-3 border border-gray-300 bg-gray-50 rounded-lg focus:ring-2 focus:ring-primary" required>
                </div>
                
                <div>
                    <button type="submit" class="w-full bg-primary text-white py-3 rounded-lg hover:bg-primary/90 transition duration-200 font-medium">تسجيل</button>
                </div>
            </form>
            
            <div class="mt-6 text-center">
                <p class="text-gray-600">لديك حساب بالفعل؟ <a href="#" id="login-link-from-register" class="text-primary hover:text-primary/80 font-medium">تسجيل الدخول</a></p>
            </div>
        </div>
    </div>

    <!-- ===== صفحة استعادة كلمة المرور ===== -->
    <div id="forgot-password-page" class="min-h-screen flex flex-col items-center justify-center px-4 py-12 hidden">
        <div class="w-full max-w-md bg-white rounded-lg shadow-lg p-8">
            <div class="text-center mb-8">
                <h1 class="font-['avenir'] text-primary text-3xl">Hyma Plastic</h1>
                <p class="text-gray-600 mt-2">استعادة كلمة المرور</p>
            </div>
            
            <form id="forgot-password-form" class="space-y-6">
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">البريد الإلكتروني</label>
                    <input type="email" id="recovery-email" class="block w-full px-4 py-3 border border-gray-300 bg-gray-50 rounded-lg focus:ring-2 focus:ring-primary" required>
                </div>
                
                <div>
                    <button type="submit" class="w-full bg-primary text-white py-3 rounded-lg hover:bg-primary/90 transition duration-200 font-medium">إرسال رابط التعيين</button>
                </div>
            </form>
            
            <div class="mt-6 text-center">
                <a href="#" id="back-to-login" class="text-primary hover:text-primary/80 font-medium">العودة إلى تسجيل الدخول</a>
            </div>
        </div>
    </div>

    <!-- ===== صفحة الخيارات الرئيسية ===== -->
    <div id="options-page" class="min-h-screen flex flex-col hidden">
        <nav class="bg-primary text-white shadow-md fixed w-full top-0 z-10">
            <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
                <h1 class="font-['avenir'] text-2xl font-bold">Hyma Plastic</h1>
                <div class="flex items-center gap-4">
                    <span class="text-sm" id="user-display-name">المستخدم</span>
                    <button id="logout-btn" class="bg-white/20 hover:bg-white/30 px-3 py-1 rounded text-sm transition">تسجيل خروج</button>
                </div>
            </div>
        </nav>

        <main class="flex-1 pt-20 pb-20">
            <div class="max-w-7xl mx-auto px-4 py-8">
                <div class="mb-12">
                    <h2 class="text-3xl font-bold text-gray-800 mb-2">أهلاً بك في النظام</h2>
                    <p class="text-gray-600">اختر أحد الخيارات التالية للبدء</p>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                    <!-- خيار 1: تقارير المبيعات -->
                    <div class="bg-white rounded-xl shadow-lg hover:shadow-2xl transition cursor-pointer p-8 option-card" data-option="sales">
                        <div class="flex justify-center mb-6">
                            <div class="w-24 h-24 rounded-full bg-blue-100 flex items-center justify-center">
                                <i class="ri-line-chart-line text-4xl text-blue-600"></i>
                            </div>
                        </div>
                        <h3 class="text-xl font-bold text-gray-800 text-center mb-2">تقارير المبيعات</h3>
                        <p class="text-gray-600 text-center text-sm mb-6">تسجيل وتتبع تقارير المبيعات والزيارات الميدانية</p>
                        <button class="w-full bg-blue-600 text-white py-2 rounded-lg hover:bg-blue-700 transition font-medium">ابدأ الآن</button>
                    </div>

                    <!-- خيار 2: شكاوى العملاء -->
                    <div class="bg-white rounded-xl shadow-lg hover:shadow-2xl transition cursor-pointer p-8 option-card" data-option="complaints">
                        <div class="flex justify-center mb-6">
                            <div class="w-24 h-24 rounded-full bg-orange-100 flex items-center justify-center">
                                <i class="ri-alert-line text-4xl text-orange-600"></i>
                            </div>
                        </div>
                        <h3 class="text-xl font-bold text-gray-800 text-center mb-2">شكاوى العملاء</h3>
                        <p class="text-gray-600 text-center text-sm mb-6">تسجيل ومتابعة شكاوى واستفسارات العملاء</p>
                        <button class="w-full bg-orange-600 text-white py-2 rounded-lg hover:bg-orange-700 transition font-medium">ابدأ الآن</button>
                    </div>

                    <!-- خيار 3: طلب عرض الأسعار -->
                    <div class="bg-white rounded-xl shadow-lg hover:shadow-2xl transition cursor-pointer p-8 option-card" data-option="quote">
                        <div class="flex justify-center mb-6">
                            <div class="w-24 h-24 rounded-full bg-green-100 flex items-center justify-center">
                                <i class="ri-file-list-line text-4xl text-green-600"></i>
                            </div>
                        </div>
                        <h3 class="text-xl font-bold text-gray-800 text-center mb-2">طلب عرض أسعار</h3>
                        <p class="text-gray-600 text-center text-sm mb-6">طلب عروض أسعار خاصة للمنتجات والخدمات</p>
                        <button class="w-full bg-green-600 text-white py-2 rounded-lg hover:bg-green-700 transition font-medium">ابدأ الآن</button>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <!-- ===== صفحة تقارير المبيعات ===== -->
    <div id="sales-page" class="min-h-screen flex flex-col hidden">
        <nav class="bg-primary text-white shadow-md fixed w-full top-0 z-10">
            <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
                <div class="flex items-center gap-4">
                    <button id="back-from-sales" class="hover:bg-white/20 p-2 rounded transition">
                        <i class="ri-arrow-right-line text-xl"></i>
                    </button>
                    <h1 class="text-lg font-bold">تقارير المبيعات</h1>
                </div>
                <div class="flex items-center gap-2">
                    <button id="sync-sales-btn" class="bg-white/20 hover:bg-white/30 px-3 py-2 rounded-lg transition flex items-center gap-2 text-sm">
                        <i class="ri-refresh-line"></i>
                        <span>مزامنة</span>
                    </button>
                    <button id="export-sales-excel" class="bg-white/20 hover:bg-white/30 px-3 py-2 rounded-lg transition flex items-center gap-2 text-sm">
                        <i class="ri-file-excel-line"></i>
                        <span>Excel</span>
                    </button>
                    <button id="export-sales-pdf" class="bg-white/20 hover:bg-white/30 px-3 py-2 rounded-lg transition flex items-center gap-2 text-sm">
                        <i class="ri-file-pdf-line"></i>
                        <span>PDF</span>
                    </button>
                    <button id="add-sales-btn" class="bg-white text-primary px-4 py-2 rounded-lg hover:bg-gray-100 transition font-medium text-sm ml-2 flex items-center gap-1">
                        <i class="ri-add-line text-xl"></i>
                        <span>إضافة تقرير</span>
                    </button>
                </div>
            </div>
        </nav>

        <!-- الزر العائم لإضافة -->
        <button id="floating-add-sales" class="fixed bottom-8 right-8 bg-primary text-white rounded-full w-16 h-16 flex items-center justify-center text-3xl shadow-lg hover:shadow-xl transition add-btn-floating z-40 hidden">
            <i class="ri-add-line"></i>
        </button>

        <main class="flex-1 pt-20 pb-16">
            <div class="max-w-7xl mx-auto px-4 py-6">
                <div class="bg-white rounded-xl shadow-lg overflow-hidden">
                    <div class="p-6 border-b border-gray-200 bg-gray-50">
                        <h2 class="text-xl font-bold text-gray-800">قائمة التقارير</h2>
                    </div>
                    <div class="overflow-x-auto">
                        <table class="w-full" id="sales-report-table">
                            <thead class="bg-gray-50 border-b">
                                <tr>
                                    <th class="px-6 py-3 text-right text-sm font-semibold text-gray-700">التاريخ</th>
                                    <th class="px-6 py-3 text-right text-sm font-semibold text-gray-700">العميل</th>
                                    <th class="px-6 py-3 text-right text-sm font-semibold text-gray-700">المبلغ</th>
                                    <th class="px-6 py-3 text-right text-sm font-semibold text-gray-700">الحالة</th>
                                    <th class="px-6 py-3 text-right text-sm font-semibold text-gray-700">الملاحظات</th>
                                </tr>
                            </thead>
                            <tbody id="sales-table" class="divide-y">
                                <tr>
                                    <td colspan="5" class="px-6 py-8 text-center text-gray-500">جاري التحميل...</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <!-- ===== صفحة إضافة تقرير مبيعات ===== -->
    <div id="add-sales-page" class="min-h-screen flex flex-col hidden">
        <nav class="bg-primary text-white shadow-md fixed w-full top-0 z-10">
            <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
                <div class="flex items-center gap-4">
                    <button id="back-from-add-sales" class="hover:bg-white/20 p-2 rounded transition">
                        <i class="ri-arrow-right-line text-xl"></i>
                    </button>
                    <h1 class="text-lg font-bold">إضافة تقرير مبيعات جديد</h1>
                </div>
                <button id="save-sales-btn" class="bg-white text-primary px-4 py-2 rounded-lg hover:bg-gray-100 transition font-medium text-sm">حفظ</button>
            </div>
        </nav>

        <main class="flex-1 pt-20 pb-16">
            <div class="max-w-4xl mx-auto px-4 py-6">
                <form id="sales-form" class="bg-white rounded-xl shadow-lg p-8 space-y-6">
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-2">اسم العميل *</label>
                            <input type="text" id="sales-client" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" required>
                        </div>
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-2">المبلغ (ريال) *</label>
                            <input type="number" id="sales-amount" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" required>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-2">التاريخ *</label>
                            <input type="date" id="sales-date" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" required>
                        </div>
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-2">الحالة *</label>
                            <select id="sales-status" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" required>
                                <option value="">اختر الحالة</option>
                                <option value="مكتمل">مكتمل</option>
                                <option value="قيد الانتظار">قيد الانتظار</option>
                                <option value="ملغى">ملغى</option>
                            </select>
                        </div>
                    </div>

                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-2">ملاحظات</label>
                        <textarea id="sales-notes" rows="4" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent"></textarea>
                    </div>
                </form>
            </div>
        </main>
    </div>

    <!-- ===== صفحة شكاوى العملاء ===== -->
    <div id="complaints-page" class="min-h-screen flex flex-col hidden">
        <nav class="bg-primary text-white shadow-md fixed w-full top-0 z-10">
            <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
                <div class="flex items-center gap-4">
                    <button id="back-from-complaints" class="hover:bg-white/20 p-2 rounded transition">
                        <i class="ri-arrow-right-line text-xl"></i>
                    </button>
                    <h1 class="text-lg font-bold">شكاوى العملاء</h1>
                </div>
                <div class="flex items-center gap-2">
                    <button id="sync-complaints-btn" class="bg-white/20 hover:bg-white/30 px-3 py-2 rounded-lg transition flex items-center gap-2 text-sm">
                        <i class="ri-refresh-line"></i>
                        <span>مزامنة</span>
                    </button>
                    <button id="export-complaints-excel" class="bg-white/20 hover:bg-white/30 px-3 py-2 rounded-lg transition flex items-center gap-2 text-sm">
                        <i class="ri-file-excel-line"></i>
                        <span>Excel</span>
                    </button>
                    <button id="export-complaints-pdf" class="bg-white/20 hover:bg-white/30 px-3 py-2 rounded-lg transition flex items-center gap-2 text-sm">
                        <i class="ri-file-pdf-line"></i>
                        <span>PDF</span>
                    </button>
                    <button id="add-complaint-btn" class="bg-white text-primary px-4 py-2 rounded-lg hover:bg-gray-100 transition font-medium text-sm ml-2 flex items-center gap-1">
                        <i class="ri-add-line text-xl"></i>
                        <span>إضافة شكوى</span>
                    </button>
                </div>
            </div>
        </nav>

        <!-- الزر العائم لإضافة -->
        <button id="floating-add-complaints" class="fixed bottom-8 right-8 bg-primary text-white rounded-full w-16 h-16 flex items-center justify-center text-3xl shadow-lg hover:shadow-xl transition add-btn-floating z-40 hidden">
            <i class="ri-add-line"></i>
        </button>

        <main class="flex-1 pt-20 pb-16">
            <div class="max-w-7xl mx-auto px-4 py-6">
                <div class="bg-white rounded-xl shadow-lg overflow-hidden">
                    <div class="p-6 border-b border-gray-200 bg-gray-50">
                        <h2 class="text-xl font-bold text-gray-800">قائمة الشكاوى</h2>
                    </div>
                    <div class="overflow-x-auto">
                        <table class="w-full" id="complaints-report-table">
                            <thead class="bg-gray-50 border-b">
                                <tr>
                                    <th class="px-6 py-3 text-right text-sm font-semibold text-gray-700">التاريخ</th>
                                    <th class="px-6 py-3 text-right text-sm font-semibold text-gray-700">العميل</th>
                                    <th class="px-6 py-3 text-right text-sm font-semibold text-gray-700">النوع</th>
                                    <th class="px-6 py-3 text-right text-sm font-semibold text-gray-700">الحالة</th>
                                    <th class="px-6 py-3 text-right text-sm font-semibold text-gray-700">الوصف</th>
                                </tr>
                            </thead>
                            <tbody id="complaints-table" class="divide-y">
                                <tr>
                                    <td colspan="5" class="px-6 py-8 text-center text-gray-500">جاري التحميل...</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <!-- ===== صفحة إضافة شكوى ===== -->
    <div id="add-complaint-page" class="min-h-screen flex flex-col hidden">
        <nav class="bg-primary text-white shadow-md fixed w-full top-0 z-10">
            <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
                <div class="flex items-center gap-4">
                    <button id="back-from-add-complaint" class="hover:bg-white/20 p-2 rounded transition">
                        <i class="ri-arrow-right-line text-xl"></i>
                    </button>
                    <h1 class="text-lg font-bold">إضافة شكوى جديدة</h1>
                </div>
                <div class="flex items-center gap-2">
                    <button id="send-complaint-email" class="bg-white/20 hover:bg-white/30 px-4 py-2 rounded-lg transition flex items-center gap-2 text-sm font-medium">
                        <i class="ri-mail-send-line"></i>
                        <span>إرسال بالايميل</span>
                    </button>
                    <button id="save-complaint-btn" class="bg-white text-primary px-4 py-2 rounded-lg hover:bg-gray-100 transition font-medium text-sm">حفظ</button>
                </div>
            </div>
        </nav>

        <main class="flex-1 pt-20 pb-16">
            <div class="max-w-4xl mx-auto px-4 py-6">
                <form id="complaint-form" class="bg-white rounded-xl shadow-lg p-8 space-y-6">
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-2">اسم العميل *</label>
                            <input type="text" id="complaint-client" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" required>
                        </div>
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-2">رقم الهاتف *</label>
                            <input type="tel" id="complaint-phone" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" required>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-2">البريد الإلكتروني *</label>
                            <input type="email" id="complaint-email" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" required>
                        </div>
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-2">نوع الشكوى *</label>
                            <select id="complaint-type" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" required>
                                <option value="">اختر النوع</option>
                                <option value="مشكلة في المنتج">مشكلة في المنتج</option>
                                <option value="مشكلة في التسليم">مشكلة في التسليم</option>
                                <option value="مشكلة في الخدمة">مشكلة في الخدمة</option>
                                <option value="مشكلة في الجودة">مشكلة في الجودة</option>
                                <option value="استفسار">استفسار</option>
                            </select>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-2">التاريخ *</label>
                            <input type="date" id="complaint-date" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" required>
                        </div>
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-2">الحالة *</label>
                            <select id="complaint-status" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" required>
                                <option value="">اختر الحالة</option>
                                <option value="مفتوح">مفتوح</option>
                                <option value="قيد المعالجة">قيد المعالجة</option>
                                <option value="تم الحل">تم الحل</option>
                            </select>
                        </div>
                    </div>

                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-2">وصف الشكوى *</label>
                        <textarea id="complaint-description" rows="4" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" required></textarea>
                    </div>
                </form>
            </div>
        </main>
    </div>

    <!-- ===== صفحة طلب عرض الأسعار ===== -->
    <div id="quote-page" class="min-h-screen flex flex-col hidden">
        <nav class="bg-primary text-white shadow-md fixed w-full top-0 z-10">
            <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
                <div class="flex items-center gap-4">
                    <button id="back-from-quote" class="hover:bg-white/20 p-2 rounded transition">
                        <i class="ri-arrow-right-line text-xl"></i>
                    </button>
                    <h1 class="text-lg font-bold">طلبات عرض الأسعار</h1>
                </div>
                <div class="flex items-center gap-2">
                    <button id="sync-quotes-btn" class="bg-white/20 hover:bg-white/30 px-3 py-2 rounded-lg transition flex items-center gap-2 text-sm">
                        <i class="ri-refresh-line"></i>
                        <span>مزامنة</span>
                    </button>
                    <button id="export-quote-excel" class="bg-white/20 hover:bg-white/30 px-3 py-2 rounded-lg transition flex items-center gap-2 text-sm">
                        <i class="ri-file-excel-line"></i>
                        <span>Excel</span>
                    </button>
                    <button id="export-quote-pdf" class="bg-white/20 hover:bg-white/30 px-3 py-2 rounded-lg transition flex items-center gap-2 text-sm">
                        <i class="ri-file-pdf-line"></i>
                        <span>PDF</span>
                    </button>
                    <button id="add-quote-btn" class="bg-white text-primary px-4 py-2 rounded-lg hover:bg-gray-100 transition font-medium text-sm ml-2 flex items-center gap-1">
                        <i class="ri-add-line text-xl"></i>
                        <span>إضافة طلب</span>
                    </button>
                </div>
            </div>
        </nav>

        <!-- الزر العائم لإضافة -->
        <button id="floating-add-quotes" class="fixed bottom-8 right-8 bg-primary text-white rounded-full w-16 h-16 flex items-center justify-center text-3xl shadow-lg hover:shadow-xl transition add-btn-floating z-40 hidden">
            <i class="ri-add-line"></i>
        </button>

        <main class="flex-1 pt-20 pb-16">
            <div class="max-w-7xl mx-auto px-4 py-6">
                <div class="bg-white rounded-xl shadow-lg overflow-hidden">
                    <div class="p-6 border-b border-gray-200 bg-gray-50">
                        <h2 class="text-xl font-bold text-gray-800">قائمة الطلبات</h2>
                    </div>
                    <div class="overflow-x-auto">
                        <table class="w-full" id="quote-report-table">
                            <thead class="bg-gray-50 border-b">
                                <tr>
                                    <th class="px-6 py-3 text-right text-sm font-semibold text-gray-700">التاريخ</th>
                                    <th class="px-6 py-3 text-right text-sm font-semibold text-gray-700">العميل</th>
                                    <th class="px-6 py-3 text-right text-sm font-semibold text-gray-700">المنتج</th>
                                    <th class="px-6 py-3 text-right text-sm font-semibold text-gray-700">الكمية</th>
                                    <th class="px-6 py-3 text-right text-sm font-semibold text-gray-700">الحالة</th>
                                </tr>
                            </thead>
                            <tbody id="quote-table" class="divide-y">
                                <tr>
                                    <td colspan="5" class="px-6 py-8 text-center text-gray-500">جاري التحميل...</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <!-- ===== صفحة إضافة طلب عرض أسعار ===== -->
    <div id="add-quote-page" class="min-h-screen flex flex-col hidden">
        <nav class="bg-primary text-white shadow-md fixed w-full top-0 z-10">
            <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
                <div class="flex items-center gap-4">
                    <button id="back-from-add-quote" class="hover:bg-white/20 p-2 rounded transition">
                        <i class="ri-arrow-right-line text-xl"></i>
                    </button>
                    <h1 class="text-lg font-bold">إضافة طلب عرض أسعار جديد</h1>
                </div>
                <button id="save-quote-btn" class="bg-white text-primary px-4 py-2 rounded-lg hover:bg-gray-100 transition font-medium text-sm">حفظ</button>
            </div>
        </nav>

        <main class="flex-1 pt-20 pb-16">
            <div class="max-w-4xl mx-auto px-4 py-6">
                <form id="quote-form" class="bg-white rounded-xl shadow-lg p-8 space-y-6">
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-2">اسم العميل *</label>
                            <input type="text" id="quote-client" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" required>
                        </div>
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-2">البريد الإلكتروني *</label>
                            <input type="email" id="quote-email" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" required>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-2">رقم الهاتف *</label>
                            <input type="tel" id="quote-phone" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" required>
                        </div>
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-2">التاريخ *</label>
                            <input type="date" id="quote-date" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" required>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-2">المنتج *</label>
                            <input type="text" id="quote-product" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" required>
                        </div>
                        <div>
                            <label class="block text-sm font-semibold text-gray-700 mb-2">الكمية *</label>
                            <input type="number" id="quote-quantity" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" required>
                        </div>
                    </div>

                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-2">وصف الطلب</label>
                        <textarea id="quote-description" rows="4" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent"></textarea>
                    </div>

                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-2">الحالة *</label>
                        <select id="quote-status" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-transparent" required>
                            <option value="">اختر الحالة</option>
                            <option value="جديد">جديد</option>
                            <option value="قيد المراجعة">قيد المراجعة</option>
                            <option value="تم الإرسال">تم الإرسال</option>
                            <option value="مقبول">مقبول</option>
                        </select>
                    </div>
                </form>
            </div>
        </main>
    </div>

    <!-- ===== نافذة النجاح ===== -->
    <div id="success-modal" class="fixed inset-0 flex items-center justify-center z-50 bg-black bg-opacity-50 hidden">
        <div class="bg-white rounded-xl p-8 w-96 text-center shadow-2xl">
            <div class="w-20 h-20 rounded-full bg-green-100 flex items-center justify-center mx-auto mb-4">
                <i class="ri-check-line text-3xl text-green-600"></i>
            </div>
            <h3 class="text-2xl font-bold text-gray-900 mb-2">تمت العملية بنجاح</h3>
            <p class="text-gray-600 mb-6" id="success-msg">تم حفظ البيانات بنجاح</p>
            <button id="close-success-btn" class="w-full bg-primary text-white py-3 rounded-lg hover:bg-primary/90 transition font-medium">حسناً</button>
        </div>
    </div>

    <!-- ===== نافذة الخطأ ===== -->
    <div id="error-modal" class="fixed inset-0 flex items-center justify-center z-50 bg-black bg-opacity-50 hidden">
        <div class="bg-white rounded-xl p-8 w-96 text-center shadow-2xl">
            <div class="w-20 h-20 rounded-full bg-red-100 flex items-center justify-center mx-auto mb-4">
                <i class="ri-close-line text-3xl text-red-600"></i>
            </div>
            <h3 class="text-2xl font-bold text-gray-900 mb-2">حدث خطأ</h3>
            <p class="text-gray-600 mb-6" id="error-msg">يرجى التحقق من البيانات والمحاولة مرة أخرى</p>
            <button id="close-error-btn" class="w-full bg-primary text-white py-3 rounded-lg hover:bg-primary/90 transition font-medium">حسناً</button>
        </div>
    </div>

    <script>
        // ===== إعدادات Google Sheets =====
        const SHEET_CONFIG = {
            SPREADSHEET_ID: 'YOUR_SPREADSHEET_ID',
            SALES_SHEET_NAME: 'تقارير المبيعات',
            COMPLAINTS_SHEET_NAME: 'شكاوى العملاء',
            QUOTES_SHEET_NAME: 'عروض الأسعار',
            WEB_APP_URL: 'YOUR_GOOGLE_APPS_SCRIPT_URL'
        };

        let salesData = [];
        let complaintsData = [];
        let quotesData = [];
        let currentUser = '';

        function showPage(pageId) {
            document.querySelectorAll('[id$="-page"]').forEach(page => page.classList.add('hidden'));
            document.getElementById(pageId).classList.remove('hidden');
            
            // إخفاء الأزرار العائمة عند تغيير الصفحة
            document.getElementById('floating-add-sales').classList.add('hidden');
            document.getElementById('floating-add-complaints').classList.add('hidden');
            document.getElementById('floating-add-quotes').classList.add('hidden');
        }

        function showSuccess(message = 'تمت العملية بنجاح') {
            document.getElementById('success-msg').textContent = message;
            document.getElementById('success-modal').classList.remove('hidden');
        }

        function showError(message = 'حدث خطأ ما') {
            document.getElementById('error-msg').textContent = message;
            document.getElementById('error-modal').classList.remove('hidden');
        }

        async function sendToGoogleSheet(sheetName, data) {
            try {
                const response = await fetch(SHEET_CONFIG.WEB_APP_URL, {
                    method: 'POST',
                    body: JSON.stringify({
                        action: 'ADD',
                        sheetName: sheetName,
                        data: data
                    })
                });
                const result = await response.json();
                return result;
            } catch (error) {
                console.error('خطأ في الاتصال:', error);
                throw error;
            }
        }

        async function getFromGoogleSheet(sheetName) {
            try {
                const response = await fetch(SHEET_CONFIG.WEB_APP_URL, {
                    method: 'POST',
                    body: JSON.stringify({
                        action: 'GET',
                        sheetName: sheetName
                    })
                });
                const result = await response.json();
                return result.data || [];
            } catch (error) {
                console.error('خطأ في استرجاع البيانات:', error);
                return [];
            }
        }

        // ===== تسجيل الدخول =====
        document.getElementById('login-form').addEventListener('submit', function(e) {
            e.preventDefault();
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;

            if (!username || !password) {
                showError('يرجى إدخال جميع البيانات');
                return;
            }

            currentUser = username;
            document.getElementById('user-display-name').textContent = username;
            loadAllData();
            showPage('options-page');
        });

        async function loadAllData() {
            try {
                const [sales, complaints, quotes] = await Promise.all([
                    getFromGoogleSheet(SHEET_CONFIG.SALES_SHEET_NAME),
                    getFromGoogleSheet(SHEET_CONFIG.COMPLAINTS_SHEET_NAME),
                    getFromGoogleSheet(SHEET_CONFIG.QUOTES_SHEET_NAME)
                ]);
                
                salesData = sales;
                complaintsData = complaints;
                quotesData = quotes;
            } catch (error) {
                console.error('خطأ في تحميل البيانات:', error);
            }
        }

        // ===== التسجيل =====
        document.getElementById('register-form').addEventListener('submit', function(e) {
            e.preventDefault();
            const pwd = document.getElementById('new-password').value;
            const confirmPwd = document.getElementById('confirm-password').value;

            if (pwd !== confirmPwd) {
                showError('كلمة المرور غير متطابقة');
                return;
            }

            showSuccess('تم إنشاء الحساب بنجاح');
            setTimeout(() => {
                document.getElementById('success-modal').classList.add('hidden');
                showPage('login-page');
            }, 2000);
        });

        // ===== استعادة كلمة المرور =====
        document.getElementById('forgot-password-form').addEventListener('submit', function(e) {
            e.preventDefault();
            showSuccess('تم إرسال رابط إعادة التعيين إلى بريدك الإلكتروني');
            setTimeout(() => {
                document.getElementById('success-modal').classList.add('hidden');
                showPage('login-page');
            }, 2000);
        });

        // ===== اختيار الخيارات =====
        document.querySelectorAll('.option-card').forEach(card => {
            card.addEventListener('click', function() {
                const option = this.getAttribute('data-option');
                if (option === 'sales') {
                    updateSalesTable();
                    showPage('sales-page');
                    document.getElementById('floating-add-sales').classList.remove('hidden');
                } else if (option === 'complaints') {
                    updateComplaintsTable();
                    showPage('complaints-page');
                    document.getElementById('floating-add-complaints').classList.remove('hidden');
                } else if (option === 'quote') {
                    updateQuotesTable();
                    showPage('quote-page');
                    document.getElementById('floating-add-quotes').classList.remove('hidden');
                }
            });
        });

        // ===== تقارير المبيعات =====
        document.getElementById('add-sales-btn').addEventListener('click', () => showPage('add-sales-page'));
        document.getElementById('floating-add-sales').addEventListener('click', () => showPage('add-sales-page'));
        document.getElementById('back-from-sales').addEventListener('click', () => showPage('options-page'));
        document.getElementById('back-from-add-sales').addEventListener('click', () => showPage('sales-page'));

        document.getElementById('save-sales-btn').addEventListener('click', function() {
            const form = document.getElementById('sales-form');
            if (!form.checkValidity()) {
                showError('يرجى ملء جميع الحقول المطلوبة');
                return;
            }

            const data = {
                التاريخ: document.getElementById('sales-date').value,
                العميل: document.getElementById('sales-client').value,
                المبلغ: document.getElementById('sales-amount').value,
                الحالة: document.getElementById('sales-status').value,
                الملاحظات: document.getElementById('sales-notes').value,
                اسم_المستخدم: currentUser,
                تاريخ_الإضافة: new Date().toLocaleString('ar-SA')
            };

            sendToGoogleSheet(SHEET_CONFIG.SALES_SHEET_NAME, data)
                .then(() => {
                    salesData.push(data);
                    showSuccess('تم حفظ التقرير بنجاح في Google Sheets');
                    form.reset();
                    setTimeout(() => {
                        document.getElementById('success-modal').classList.add('hidden');
                        showPage('sales-page');
                        updateSalesTable();
                        document.getElementById('floating-add-sales').classList.remove('hidden');
                    }, 1500);
                })
                .catch(() => {
                    showError('فشل حفظ البيانات. تأكد من إعدادات Google Sheets');
                });
        });

        document.getElementById('sync-sales-btn').addEventListener('click', async () => {
            try {
                const data = await getFromGoogleSheet(SHEET_CONFIG.SALES_SHEET_NAME);
                salesData = data;
                updateSalesTable();
                showSuccess('تمت المزامنة بنجاح');
            } catch (error) {
                showError('فشلت المزامنة');
            }
        });

        document.getElementById('export-sales-excel').addEventListener('click', function() {
            if (salesData.length === 0) {
                showError('لا توجد بيانات للتصدير');
                return;
            }
            const ws = XLSX.utils.json_to_sheet(salesData);
            const wb = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(wb, ws, 'تقارير المبيعات');
            XLSX.writeFile(wb, 'تقارير_المبيعات.xlsx');
            showSuccess('تم تصدير البيانات بنجاح');
        });

        document.getElementById('export-sales-pdf').addEventListener('click', function() {
            if (salesData.length === 0) {
                showError('لا توجد بيانات للتصدير');
                return;
            }
            const element = document.getElementById('sales-report-table');
            const opt = {
                margin: 10,
                filename: 'تقارير_المبيعات.pdf',
                image: { type: 'jpeg', quality: 0.98 },
                html2canvas: { scale: 2 },
                jsPDF: { orientation: 'landscape', unit: 'mm', format: 'a4' }
            };
            html2pdf().set(opt).from(element).save();
            showSuccess('تم تصدير ملف PDF بنجاح');
        });

        // ===== شكاوى العملاء =====
        document.getElementById('add-complaint-btn').addEventListener('click', () => showPage('add-complaint-page'));
        document.getElementById('floating-add-complaints').addEventListener('click', () => showPage('add-complaint-page'));
        document.getElementById('back-from-complaints').addEventListener('click', () => showPage('options-page'));
        document.getElementById('back-from-add-complaint').addEventListener('click', () => showPage('complaints-page'));

        document.getElementById('save-complaint-btn').addEventListener('click', function() {
            const form = document.getElementById('complaint-form');
            if (!form.checkValidity()) {
                showError('يرجى ملء جميع الحقول المطلوبة');
                return;
            }

            const data = {
                التاريخ: document.getElementById('complaint-date').value,
                العميل: document.getElementById('complaint-client').value,
                رقم_الهاتف: document.getElementById('complaint-phone').value,
                البريد_الإلكتروني: document.getElementById('complaint-email').value,
                النوع: document.getElementById('complaint-type').value,
                الحالة: document.getElementById('complaint-status').value,
                الوصف: document.getElementById('complaint-description').value,
                اسم_المستخدم: currentUser,
                تاريخ_الإضافة: new Date().toLocaleString('ar-SA')
            };

            sendToGoogleSheet(SHEET_CONFIG.COMPLAINTS_SHEET_NAME, data)
                .then(() => {
                    complaintsData.push(data);
                    showSuccess('تم إضافة الشكوى بنجاح في Google Sheets');
                    form.reset();
                    setTimeout(() => {
                        document.getElementById('success-modal').classList.add('hidden');
                        showPage('complaints-page');
                        updateComplaintsTable();
                        document.getElementById('floating-add-complaints').classList.remove('hidden');
                    }, 1500);
                })
                .catch(() => {
                    showError('فشل حفظ الشكوى. تأكد من إعدادات Google Sheets');
                });
        });

        document.getElementById('sync-complaints-btn').addEventListener('click', async () => {
            try {
                const data = await getFromGoogleSheet(SHEET_CONFIG.COMPLAINTS_SHEET_NAME);
                complaintsData = data;
                updateComplaintsTable();
                showSuccess('تمت المزامنة بنجاح');
            } catch (error) {
                showError('فشلت المزامنة');
            }
        });

        document.getElementById('send-complaint-email').addEventListener('click', function() {
            const form = document.getElementById('complaint-form');
            if (!form.checkValidity()) {
                showError('يرجى ملء جميع الحقول المطلوبة أولاً');
                return;
            }

            const email = document.getElementById('complaint-email').value;
            const client = document.getElementById('complaint-client').value;
            const subject = encodeURIComponent('شكوى جديدة من ' + client);
            const body = encodeURIComponent(`
اسم العميل: ${document.getElementById('complaint-client').value}
رقم الهاتف: ${document.getElementById('complaint-phone').value}
نوع الشكوى: ${document.getElementById('complaint-type').value}
التاريخ: ${document.getElementById('complaint-date').value}
الحالة: ${document.getElementById('complaint-status').value}

وصف الشكوى:
${document.getElementById('complaint-description').value}
            `);

            window.location.href = `mailto:${email}?subject=${subject}&body=${body}`;
            showSuccess('تم فتح تطبيق البريد الإلكتروني');
        });

        // تصدير شكاوى العملاء
        document.getElementById('export-complaints-excel').addEventListener('click', function() {
            if (complaintsData.length === 0) {
                showError('لا توجد بيانات للتصدير');
                return;
            }
            const ws = XLSX.utils.json_to_sheet(complaintsData);
            const wb = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(wb, ws, 'الشكاوى');
            XLSX.writeFile(wb, 'شكاوى_العملاء.xlsx');
            showSuccess('تم تصدير البيانات بنجاح');
        });

        document.getElementById('export-complaints-pdf').addEventListener('click', function() {
            if (complaintsData.length === 0) {
                showError('لا توجد بيانات للتصدير');
                return;
            }
            const element = document.getElementById('complaints-report-table');
            const opt = {
                margin: 10,
                filename: 'شكاوى_العملاء.pdf',
                image: { type: 'jpeg', quality: 0.98 },
                html2canvas: { scale: 2 },
                jsPDF: { orientation: 'landscape', unit: 'mm', format: 'a4' }
            };
            html2pdf().set(opt).from(element).save();
            showSuccess('تم تصدير ملف PDF بنجاح');
        });

        // ===== طلبات عرض الأسعار =====
document.getElementById('add-quote-btn').addEventListener('click', () => showPage('add-quote-page'));
document.getElementById('floating-add-quotes').addEventListener('click', () => showPage('add-quote-page'));
document.getElementById('back-from-quote').addEventListener('click', () => showPage('options-page'));
document.getElementById('back-from-add-quote').addEventListener('click', () => showPage('quote-page'));

document.getElementById('save-quote-btn').addEventListener('click', function() {
    const form = document.getElementById('quote-form');
    if (!form.checkValidity()) {
        showError('يرجى ملء جميع الحقول ��لمطلوبة');
        return;
    }

    const data = {
        التاريخ: document.getElementById('quote-date').value,
        العميل: document.getElementById('quote-client').value,
        البريد_الإلكتروني: document.getElementById('quote-email').value,
        رقم_الهاتف: document.getElementById('quote-phone').value,
        المنتج: document.getElementById('quote-product').value,
        الكمية: document.getElementById('quote-quantity').value,
        الوصف: document.getElementById('quote-description').value,
        الحالة: document.getElementById('quote-status').value,
        اسم_المستخدم: currentUser,
        تاريخ_الإضافة: new Date().toLocaleString('ar-SA')
    };

    sendToGoogleSheet(SHEET_CONFIG.QUOTES_SHEET_NAME, data)
        .then(() => {
            quotesData.push(data);
            showSuccess('تم إضافة الطلب بنجاح في Google Sheets');
            form.reset();
            setTimeout(() => {
                document.getElementById('success-modal').classList.add('hidden');
                showPage('quote-page');
                updateQuotesTable();
                document.getElementById('floating-add-quotes').classList.remove('hidden');
            }, 1500);
        })
        .catch(() => {
            showError('فشل حفظ الطلب. تأكد من إعدادات Google Sheets');
        });
});

document.getElementById('sync-quotes-btn').addEventListener('click', async () => {
    try {
        const data = await getFromGoogleSheet(SHEET_CONFIG.QUOTES_SHEET_NAME);
        quotesData = data;
        updateQuotesTable();
        showSuccess('تمت المزامنة بنجاح');
    } catch (error) {
        showError('فشلت المزامنة');
    }
});

// تصدير طلبات الأسعار
document.getElementById('export-quote-excel').addEventListener('click', function() {
    if (quotesData.length === 0) {
        showError('لا توجد بيانات للتصدير');
        return;
    }
    const ws = XLSX.utils.json_to_sheet(quotesData);
    const wb = XLSX.utils.book_new();
    XLSX.utils.book_append_sheet(wb, ws, 'عروض الأسعار');
    XLSX.writeFile(wb, 'عروض_الأسعار.xlsx');
    showSuccess('تم تصدير البيانات بنجاح');
});

document.getElementById('export-quote-pdf').addEventListener('click', function() {
    if (quotesData.length === 0) {
        showError('لا توجد بيانات للتصدير');
        return;
    }
    const element = document.getElementById('quote-report-table');
    const opt = {
        margin: 10,
        filename: 'عروض_الأسعار.pdf',
        image: { type: 'jpeg', quality: 0.98 },
        html2canvas: { scale: 2 },
        jsPDF: { orientation: 'landscape', unit: 'mm', format: 'a4' }
    };
    html2pdf().set(opt).from(element).save();
    showSuccess('تم تصدير ملف PDF بنجاح');
});

// ===== تحديث الجداول - النسخة الصحيحة =====
function updateSalesTable() {
    const tbody = document.getElementById('sales-table');
    if (salesData.length === 0) {
        tbody.innerHTML = '<tr><td colspan="5" class="px-6 py-8 text-center text-gray-500">لا توجد تقارير بعد</td></tr>';
        return;
    }
    tbody.innerHTML = salesData.map(item => `
        <tr class="border-b hover:bg-gray-50">
            <td class="px-6 py-4 text-sm text-gray-700">${item.التاريخ || item.date || ''}</td>
            <td class="px-6 py-4 text-sm text-gray-700">${item.العميل || item.client || ''}</td>
            <td class="px-6 py-4 text-sm text-gray-700">${item.المبلغ || item.amount || ''}</td>
            <td class="px-6 py-4 text-sm"><span class="px-3 py-1 bg-blue-100 text-blue-800 rounded-full text-xs font-semibold">${item.الحالة || item.status || ''}</span></td>
            <td class="px-6 py-4 text-sm text-gray-700 truncate">${item.الملاحظات || item.notes || ''}</td>
        </tr>
    `).join('');
}

function updateComplaintsTable() {
    const tbody = document.getElementById('complaints-table');
    if (complaintsData.length === 0) {
        tbody.innerHTML = '<tr><td colspan="5" class="px-6 py-8 text-center text-gray-500">لا توجد شكاوى بعد</td></tr>';
        return;
    }
    tbody.innerHTML = complaintsData.map(item => `
        <tr class="border-b hover:bg-gray-50">
            <td class="px-6 py-4 text-sm text-gray-700">${item.التاريخ || item.date || ''}</td>
            <td class="px-6 py-4 text-sm text-gray-700">${item.العميل || item.client || ''}</td>
            <td class="px-6 py-4 text-sm text-gray-700">${item.النوع || item.type || ''}</td>
            <td class="px-6 py-4 text-sm"><span class="px-3 py-1 bg-orange-100 text-orange-800 rounded-full text-xs font-semibold">${item.الحالة || item.status || ''}</span></td>
            <td class="px-6 py-4 text-sm text-gray-700 truncate">${item.الوصف || item.description || ''}</td>
        </tr>
    `).join('');
}

// ✅ النسخة الصحيحة للدالة - استخدام quotesData وليس salesData
function updateQuotesTable() {
    const tbody = document.getElementById('quote-table');
    if (quotesData.length === 0) {
        tbody.innerHTML = '<tr><td colspan="5" class="px-6 py-8 text-center text-gray-500">لا توجد طلبات بعد</td></tr>';
        return;
    }
    tbody.innerHTML = quotesData.map(item => `
        <tr class="border-b hover:bg-gray-50">
            <td class="px-6 py-4 text-sm text-gray-700">${item.التاريخ || item.date || ''}</td>
            <td class="px-6 py-4 text-sm text-gray-700">${item.العميل || item.client || ''}</td>
            <td class="px-6 py-4 text-sm text-gray-700">${item.المنتج || item.product || ''}</td>
            <td class="px-6 py-4 text-sm text-gray-700">${item.الكمية || item.quantity || ''}</td>
            <td class="px-6 py-4 text-sm"><span class="px-3 py-1 bg-green-100 text-green-800 rounded-full text-xs font-semibold">${item.الحالة || item.status || ''}</span></td>
        </tr>
    `).join('');
}

        function updateComplaintsTable() {
            const tbody = document.getElementById('complaints-table');
            if (complaintsData.length === 0) {
                tbody.innerHTML = '<tr><td colspan="5" class="px-6 py-8 text-center text-gray-500">لا توجد شكاوى بعد</td></tr>';
                return;
            }
            tbody.innerHTML = complaintsData.map(item => `
                <tr class="border-b hover:bg-gray-50">
                    <td class="px-6 py-4 text-sm text-gray-700">${item.date}</td>
                    <td class="px-6 py-4 text-sm text-gray-700">${item.client}</td>
                    <td class="px-6 py-4 text-sm text-gray-700">${item.type}</td>
                    <td class="px-6 py-4 text-sm"><span class="px-3 py-1 bg-orange-100 text-orange-800 rounded-full text-xs font-semibold">${item.status}</span></td>
                    <td class="px-6 py-4 text-sm text-gray-700 truncate">${item.description}</td>
                </tr>
            `).join('');
        }

        function updateQuotesTable() {
            const tbody = document.getElementById('quote-table');
            if (quotesData.length === 0) {
                tbody.innerHTML = '<tr><td colspan="5" class="px-6 py-8 text-center text-gray-500">لا توجد طلبات بعد</td></tr>';
                return;
            }
            tbody.innerHTML = salesData.map(item => `
                <tr class="border-b hover:bg-gray-50">
                    <td class="px-6 py-4 text-sm text-gray-700">${item.date}</td>
                    <td class="px-6 py-4 text-sm text-gray-700">${item.client}</td>
                    <td class="px-6 py-4 text-sm text-gray-700">${item.amount}</td>
                    <td class="px-6 py-4 text-sm"><span class="px-3 py-1 bg-blue-100 text-blue-800 rounded-full text-xs font-semibold">${item.status}</span></td>
                    <td class="px-6 py-4 text-sm"><button class="text-primary hover:text-primary/70">عرض</button></td>
                </tr>
            `).join('');
        }

        function updateComplaintsTable() {
            const tbody = document.getElementById('complaints-table');
            if (complaintsData.length === 0) {
                tbody.innerHTML = '<tr><td colspan="5" class="px-6 py-8 text-center text-gray-500">لا توجد شكاوى بعد</td></tr>';
                return;
            }
            tbody.innerHTML = complaintsData.map(item => `
                <tr class="border-b hover:bg-gray-50">
                    <td class="px-6 py-4 text-sm text-gray-700">${item.date}</td>
                    <td class="px-6 py-4 text-sm text-gray-700">${item.client}</td>
                    <td class="px-6 py-4 text-sm text-gray-700">${item.type}</td>
                    <td class="px-6 py-4 text-sm"><span class="px-3 py-1 bg-orange-100 text-orange-800 rounded-full text-xs font-semibold">${item.status}</span></td>
                    <td class="px-6 py-4 text-sm"><button class="text-primary hover:text-primary/70">عرض</button></td>
                </tr>
            `).join('');
        }

        function updateQuotesTable() {
            const tbody = document.getElementById('quote-table');
            if (quotesData.length === 0) {
                tbody.innerHTML = '<tr><td colspan="6" class="px-6 py-8 text-center text-gray-500">لا توجد طلبات بعد</td></tr>';
                return;
            }
            tbody.innerHTML = quotesData.map(item => `
                <tr class="border-b hover:bg-gray-50">
                    <td class="px-6 py-4 text-sm text-gray-700">${item.date}</td>
                    <td class="px-6 py-4 text-sm text-gray-700">${item.client}</td>
                    <td class="px-6 py-4 text-sm text-gray-700">${item.product}</td>
                    <td class="px-6 py-4 text-sm text-gray-700">${item.quantity}</td>
                    <td class="px-6 py-4 text-sm"><span class="px-3 py-1 bg-green-100 text-green-800 rounded-full text-xs font-semibold">${item.status}</span></td>
                    <td class="px-6 py-4 text-sm"><button class="text-primary hover:text-primary/70">عرض</button></td>
                </tr>
            `).join('');
        }

        // الأزرار العامة
        document.getElementById('register-link').addEventListener('click', e => {
            e.preventDefault();
            showPage('register-page');
        });

        document.getElementById('login-link-from-register').addEventListener('click', e => {
            e.preventDefault();
            showPage('login-page');
        });

        document.getElementById('forgot-password-link').addEventListener('click', e => {
            e.preventDefault();
            showPage('forgot-password-page');
        });

        document.getElementById('back-to-login').addEventListener('click', e => {
            e.preventDefault();
            showPage('login-page');
        });

        document.getElementById('logout-btn').addEventListener('click', () => showPage('login-page'));

        document.getElementById('close-success-btn').addEventListener('click', () => {
            document.getElementById('success-modal').classList.add('hidden');
        });

        document.getElementById('close-error-btn').addEventListener('click', () => {
            document.getElementById('error-modal').classList.add('hidden');
        });
    </script>
</body>
</html>
