<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="description" content="نظام إدارة المبيعات - Hyma Plastic">
    <meta name="theme-color" content="#6366f1">
    <title>Hyma Plastic - نظام إدارة المبيعات المتكامل</title>
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com/3.4.16 "></script>
    <!-- SheetJS -->
    <script src="https://cdn.sheetjs.com/xlsx-0.20.2/package/dist/xlsx.full.min.js "></script>
    <!-- Remix Icon -->
    <link href="https://cdnjs.cloudflare.com/ajax/libs/remixicon/4.6.0/remixicon.min.css " rel="stylesheet">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300 ;400;500;600;700;800&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: { 
                        primary: '#166534',
                        primaryDark: '#059669',
                        primaryLight: '#34d399',
                        secondary: '#1e293b',
                        accent: '#f59e0b',
                        success: '#10b981',
                        danger: '#ef4444',
                        warning: '#f59e0b',
                        info: '#3b82f6'
                    },
                    fontFamily: {
                        sans: ['Inter', 'Tajawal', 'system-ui', 'sans-serif'],
                    },
                    boxShadow: {
                        'soft': '0 4px 20px -2px rgba(0, 0, 0, 0.05)',
                        'card': '0 20px 35px -12px rgba(0, 0, 0, 0.08)',
                        'hover': '0 25px 40px -12px rgba(99, 102, 241, 0.25)',
                    },
                    animation: {
                        'fade-in': 'fadeIn 0.3s ease-out',
                        'slide-up': 'slideUp 0.4s ease-out',
                        'pulse-slow': 'pulse 3s cubic-bezier(0.4, 0, 0.6, 1) infinite',
                        'shimmer': 'shimmer 1.5s infinite',
                    },
                    keyframes: {
                        fadeIn: {
                            '0%': { opacity: '0' },
                            '100%': { opacity: '1' },
                        },
                        slideUp: {
                            '0%': { transform: 'translateY(20px)', opacity: '0' },
                            '100%': { transform: 'translateY(0)', opacity: '1' },
                        },
                        shimmer: {
                            '0%': { backgroundPosition: '-200% 0' },
                            '100%': { backgroundPosition: '200% 0' },
                        }
                    }
                }
            }
        }
    </script>
    
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Tajawal:wght@300 ;400;500;700;800&display=swap');
        
        * {
            -webkit-tap-highlight-color: transparent;
            scroll-behavior: smooth;
        }
        
        body {
            font-family: 'Inter', 'Tajawal', sans-serif;
            background: linear-gradient(135deg, #f8fafc 0%, #eff6ff 100%);
            min-height: 100vh;
            overflow-x: hidden;
        }
        
        /* Modern Scrollbar */
        ::-webkit-scrollbar { width: 8px; height: 8px; }
        ::-webkit-scrollbar-track { background: #f1f5f9; border-radius: 10px; }
        ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 10px; }
        ::-webkit-scrollbar-thumb:hover { background: #94a3b8; }
        
        /* Modern Card Styles */
        .modern-card {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.3);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        
        .modern-card:hover {
            transform: translateY(-4px);
            box-shadow: 0 25px 40px -12px rgba(99, 102, 241, 0.25);
            border-color: rgba(99, 102, 241, 0.3);
        }
        
        /* Modern Button */
        .btn-modern {
            position: relative;
            overflow: hidden;
            transition: all 0.3s ease;
            background: linear-gradient(135deg, #6366f1, #4f46e5);
        }
        
        .btn-modern::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
            transition: left 0.5s;
        }
        
        .btn-modern:hover::before {
            left: 100%;
        }
        
        /* Modern Table */
        .modern-table {
            border-collapse: separate;
            border-spacing: 0;
            width: 100%;
        }
        
        .modern-table thead tr {
            background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
        }
        
        .modern-table th {
            padding: 1rem 1.5rem;
            font-weight: 600;
            color: #1e293b;
            border-bottom: 2px solid #e2e8f0;
        }
        
        .modern-table td {
            padding: 1rem 1.5rem;
            border-bottom: 1px solid #f1f5f9;
            transition: all 0.2s;
        }
        
        .modern-table tbody tr:hover {
            background: linear-gradient(90deg, #f8fafc, #ffffff);
        }
        
        /* Badge Styles */
        .badge {
            display: inline-flex;
            align-items: center;
            padding: 0.375rem 0.875rem;
            border-radius: 9999px;
            font-size: 0.75rem;
            font-weight: 700;
            letter-spacing: 0.025em;
        }
        .badge-approved { background: #dcfce7; color: #166534; }
        .badge-pending { background: #fef9c3; color: #854d0e; }
        .badge-rejected { background: #fee2e2; color: #991b1b; }
        
        /* Table Container */
        .table-container {
            background: white;
            border-radius: 1rem;
            box-shadow: 0 4px 20px -2px rgba(0, 0, 0, 0.05);
            overflow: hidden;
            border: 1px solid #e2e8f0;
        }
        
        /* Dropdown Styles */
        .profile-dropdown, .notifications-dropdown {
            position: absolute;
            top: 100%;
            left: 0;
            margin-top: 0.5rem;
            background: white;
            border-radius: 1rem;
            box-shadow: 0 20px 35px -8px rgba(0,0,0,0.15);
            min-width: 240px;
            z-index: 100;
            border: 1px solid #e2e8f0;
            overflow: hidden;
        }
        
        .profile-dropdown a, .profile-dropdown button, .notifications-dropdown .notif-item {
            display: flex;
            align-items: center;
            gap: 0.75rem;
            padding: 0.75rem 1rem;
            transition: all 0.2s;
            font-size: 0.9rem;
            color: #334155;
            width: 100%;
            text-align: right;
            border-bottom: 1px solid #f1f5f9;
        }
        
        .profile-dropdown a:hover, .profile-dropdown button:hover, .notifications-dropdown .notif-item:hover {
            background: #f0fdf4;
            color: #059669;
        }
        
        .notif-badge {
            position: absolute;
            top: -5px;
            right: -5px;
            background: #ef4444;
            color: white;
            border-radius: 9999px;
            font-size: 0.7rem;
            min-width: 18px;
            height: 18px;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 0 4px;
            font-weight: bold;
        }
        
        /* Loading Spinner */
        .skeleton {
            background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
            background-size: 200% 100%;
            animation: shimmer 1.5s infinite;
        }
        
        /* Modal Backdrop */
        .modal-backdrop {
            background: rgba(0, 0, 0, 0.6);
            backdrop-filter: blur(4px);
        }
        
        /* Animation */
        @keyframes shimmer {
            0% { background-position: -200% 0; }
            100% { background-position: 200% 0; }
        }
        
        @keyframes marquee {
            0% { transform: translateX(100%); }
            100% { transform: translateX(-100%); }
        }
        
        .marquee-text {
            display: inline-block;
            white-space: nowrap;
            animation: marquee 25s linear infinite;
        }
        
        .marquee-container {
            overflow: hidden;
            white-space: nowrap;
            width: 100%;
        }
        
        @media print {
            body * { visibility: hidden; }
            .print-only, .print-only * { visibility: visible; }
            .print-only { position: absolute; top: 0; right: 0; width: 100%; }
        }
        
        .watermark { position: relative; }
        .watermark::after {
            content: "DRAFT";
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) rotate(-30deg);
            font-size: 80px;
            font-weight: bold;
            color: rgba(0,0,0,0.05);
            pointer-events: none;
            white-space: nowrap;
        }
        
        /* Dark Mode */
        .dark body {
            background: linear-gradient(135deg, #0f172a 0%, #1e293b 100%);
        }
        
        .dark .modern-card {
            background: rgba(30, 41, 59, 0.95);
            border-color: rgba(255, 255, 255, 0.1);
        }
        
        .dark .table-container {
            background: #1e293b;
            border-color: #334155;
        }
        
        .dark .modern-table td {
            border-bottom-color: #334155;
            color: #e2e8f0;
        }
        
        .dark .modern-table th {
            background: #0f172a;
            color: #e2e8f0;
        }
    </style>
</head>
<body class="bg-gray-50 text-slate-800 dark:bg-gray-900 dark:text-slate-200">

<!-- ============================================== -->
<!--                     Login Page                 -->
<!-- ============================================== -->
<div id="login-page" class="min-h-screen flex items-center justify-center px-4 relative bg-cover bg-center" style="background-image: url('https://up6.cc/2026/03/177244201974711.jpg ');">
    <div class="absolute inset-0 bg-black/20"></div>
    <div class="w-full max-w-md bg-white/95 dark:bg-gray-800/95 backdrop-blur-xl rounded-3xl shadow-2xl p-8 relative z-10 border border-white/20 animate-slide-up">
        <div class="text-center mb-8">
            <div class="mb-6 relative inline-block">
                <div class="absolute inset-0 bg-primary/20 rounded-full blur-xl"></div>
                <img src="https://g.top4top.io/p_3708dgdoj1.png " alt="Hyma Logo" class="w-28 h-28 mx-auto relative z-10 drop-shadow-lg">
            </div>
<h1 class="font-bold text-4xl text-primary mb-2">Hyma Plastic</h1>
            <p class="text-gray-500 dark:text-gray-400 text-lg font-medium">نظام إدارة المبيعات المتكامل</p>
        </div>
        
        <form id="login-form" class="space-y-5">
            <div class="relative">
                <label class="block text-sm font-semibold text-gray-700 dark:text-gray-300 mb-2 mr-1">اسم المستخدم</label>
                <div class="relative">
                    <i class="ri-user-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                    <input type="text" id="username" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 dark:border-gray-700 dark:bg-gray-900 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all text-base bg-gray-50/50" placeholder="أدخل اسم المستخدم" required>
                </div>
            </div>
            <div class="relative">
                <label class="block text-sm font-semibold text-gray-700 dark:text-gray-300 mb-2 mr-1">كلمة المرور</label>
                <div class="relative">
                    <i class="ri-lock-password-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                    <input type="password" id="password" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 dark:border-gray-700 dark:bg-gray-900 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all text-base bg-gray-50/50" placeholder="أدخل كلمة المرور" required>
                </div>
            </div>
                <button type="submit" id="login-btn" class="w-full bg-primary hover:bg-primaryDark text-white py-4 rounded-xl font-bold text-lg shadow-lg shadow-primary/30 hover:shadow-xl hover:shadow-primary/40 transform hover:-translate-y-0.5 transition-all duration-300 flex items-center justify-center gap-2">
                <span>تسجيل الدخول</span>
                <i class="ri-login-box-line text-xl"></i>
            </button>
        </form>
        
        <div class="mt-8 text-center">
            <a id="register-link" href="#" class="inline-flex items-center gap-2 text-primary hover:text-primaryDark font-semibold transition-colors text-sm hover:gap-3 duration-300">
                <i class="ri-user-add-line text-lg"></i>
                <span>تسجيل مستخدم جديد</span>
                <i class="ri-arrow-left-line"></i>
            </a>
        </div>
        
        <form id="register-form" class="space-y-4 hidden mt-6 animate-fade-in">
            <div class="space-y-4">
                <div class="relative">
                    <i class="ri-user-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400"></i>
                    <input type="text" id="register-username" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 dark:border-gray-700 dark:bg-gray-900 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all" placeholder="اسم المستخدم" required>
                </div>
                <div class="relative">
                    <i class="ri-mail-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400"></i>
                    <input type="email" id="register-email" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 dark:border-gray-700 dark:bg-gray-900 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all" placeholder="البريد الإلكتروني" required>
                </div>
                <div class="relative">
                    <i class="ri-lock-password-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400"></i>
                    <input type="password" id="register-password" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 dark:border-gray-700 dark:bg-gray-900 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all" placeholder="كلمة المرور" required>
                </div>
                <div class="relative">
                    <i class="ri-lock-password-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400"></i>
                    <input type="password" id="register-confirm-password" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 dark:border-gray-700 dark:bg-gray-900 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all" placeholder="تأكيد كلمة المرور" required>
                </div>
            </div>
<button type="submit" class="w-full bg-primary hover:bg-primaryDark text-white py-3.5 rounded-xl font-bold shadow-lg shadow-primary/30 hover:shadow-xl hover:shadow-primary/40 transition-all duration-300 flex items-center justify-center gap-2">
                طلب إنشاء حساب
            </button>
            <p class="text-xs text-gray-500 text-center bg-gray-50 dark:bg-gray-800 py-2 rounded-lg">سيتم مراجعة طلبك من قبل المسؤول</p>
        </form>
        
        <div id="login-link-container" class="hidden mt-4 text-center animate-fade-in">
            <a id="login-link" href="#" class="inline-flex items-center gap-2 text-primary hover:text-primaryDark font-semibold transition-colors text-sm">
                <i class="ri-login-box-line"></i>
                <span>هل لديك حساب؟ سجل دخول</span>
                <i class="ri-arrow-left-line"></i>
            </a>
        </div>
        
        <div class="mt-8 text-center text-xs text-gray-400 border-t border-gray-200 dark:border-gray-700 pt-4">
            <p>Copyright 2026 - HymaPlastic. All rights reserved ©</p>
            <p class="mt-1 text-primary/90 font-medium">By: Eng - Haitham Elsaqqa</p>
        </div>
    </div>
</div>

<!-- لوحة تحكم المسؤول / المدير -->
    <div id="admin-page" class="min-h-screen flex flex-col hidden page-transition bg-gradient-to-br from-gray-50 to-slate-100">
        <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
            <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
                <div class="flex items-center gap-4">
                    <div class="bg-white/20 p-2.5 rounded-xl backdrop-blur-sm">
                        <i class="ri-admin-line text-2xl"></i>
                    </div>
                    <div>
                        <h1 class="text-2xl font-bold tracking-tight">لوحة التحكم</h1>
                        <p class="text-white/70 text-xs">نظام إدارة المبيعات</p>
                    </div>
                    <button onclick="openMessagesModal()" class="bg-white/10 hover:bg-white/20 backdrop-blur-sm px-4 py-2 rounded-xl text-sm flex items-center gap-2 transition-all border border-white/10 hover:border-white/30" title="إدارة رسائل المسؤول">
                        <i class="ri-message-2-line text-lg"></i>
                        <span class="hidden sm:inline font-medium">الرسائل</span>
                    </button>
                    <button onclick="openPriceListModal()" class="bg-gradient-to-r from-red-500 to-red-600 hover:from-red-600 hover:to-red-700 text-white px-4 py-2 rounded-xl text-sm flex items-center gap-2 transition-all shadow-lg shadow-red-500/30" title="قائمة الأسعار">
                        <i class="ri-price-tag-3-line text-lg"></i>
                        <span class="hidden sm:inline font-medium">قائمة الأسعار</span>
                    </button>
                </div>
                <div class="flex items-center gap-4">
                    <div class="hidden md:flex flex-col items-end">
                        <span id="admin-user-name" class="text-sm font-bold"></span>
                        <span id="admin-user-role" class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm"></span>
                    </div>
                    <button id="admin-logout" class="bg-white/10 hover:bg-white/20 backdrop-blur-sm px-5 py-2.5 rounded-xl transition-all border border-white/10 hover:border-white/30 flex items-center gap-2 font-medium">
                        <i class="ri-logout-box-r-line"></i>
                        <span>-----</span>
                    </button>
                </div>
            </div>
        </nav>

        <main class="flex-1 pt-28 pb-16 px-4">
            <div class="max-w-7xl mx-auto">
                <!-- الإحصائيات (8 كروت) -->
                <div class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 gap-4 md:gap-6 mb-8">
                    <!-- 1. العملاء -->
                    <div class="stats-card bg-white p-5 shadow-card hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-1 border border-gray-100">
                        <div class="flex items-center justify-between mb-4">
                            <div class="p-3 bg-gradient-to-br from-purple-500 to-purple-600 rounded-xl shadow-lg shadow-purple-500/30">
                                <i class="ri-user-star-line text-2xl text-white"></i>
                            </div>
                            <span class="text-xs font-bold text-purple-600 bg-purple-50 px-2 py-1 rounded-full">العملاء</span>
                        </div>
                        <h3 class="text-3xl font-bold text-gray-800 mb-1" id="stats-total-customers">0</h3>
                        <p class="text-xs text-gray-500">عميل مسجل</p>
                    </div>
                    
                    <!-- 2. الخطط -->
                    <div class="stats-card bg-white p-5 shadow-card hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-1 border border-gray-100">
                        <div class="flex items-center justify-between mb-4">
                            <div class="p-3 bg-gradient-to-br from-cyan-500 to-cyan-600 rounded-xl shadow-lg shadow-cyan-500/30">
                                <i class="ri-calendar-todo-line text-2xl text-white"></i>
                            </div>
                            <span class="text-xs font-bold text-cyan-600 bg-cyan-50 px-2 py-1 rounded-full">الخطط</span>
                        </div>
                        <h3 class="text-3xl font-bold text-gray-800 mb-1" id="stats-total-plans">0</h3>
                        <p class="text-xs text-gray-500">خطة أسبوعية</p>
                    </div>
                    
                    <!-- 3. الزيارات -->
                    <div class="stats-card bg-white p-5 shadow-card hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-1 border border-gray-100">
                        <div class="flex items-center justify-between mb-4">
                            <div class="p-3 bg-gradient-to-br from-indigo-500 to-indigo-600 rounded-xl shadow-lg shadow-indigo-500/30">
                                <i class="ri-user-location-line text-2xl text-white"></i>
                            </div>
                            <span class="text-xs font-bold text-indigo-600 bg-indigo-50 px-2 py-1 rounded-full">الزيارات</span>
                        </div>
                        <h3 class="text-3xl font-bold text-gray-800 mb-1" id="stats-total-visits">0</h3>
                        <p class="text-xs text-gray-500">زيارة ميدانية</p>
                    </div>
                    
                    <!-- 4. الأنشطة -->
                    <div class="stats-card bg-white p-5 shadow-card hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-1 border border-gray-100">
                        <div class="flex items-center justify-between mb-4">
                            <div class="p-3 bg-gradient-to-br from-teal-500 to-teal-600 rounded-xl shadow-lg shadow-teal-500/30">
                                <i class="ri-calendar-check-line text-2xl text-white"></i>
                            </div>
                            <span class="text-xs font-bold text-teal-600 bg-teal-50 px-2 py-1 rounded-full">الأنشطة</span>
                        </div>
                        <h3 class="text-3xl font-bold text-gray-800 mb-1" id="stats-total-activities">0</h3>
                        <p class="text-xs text-gray-500">نشاط يومي</p>
                    </div>
                    
                    <!-- 5. عروض الأسعار -->
                    <div class="stats-card bg-white p-5 shadow-card hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-1 border border-gray-100">
                        <div class="flex items-center justify-between mb-4">
                            <div class="p-3 bg-gradient-to-br from-green-500 to-green-600 rounded-xl shadow-lg shadow-green-500/30">
                                <i class="ri-file-list-line text-2xl text-white"></i>
                            </div>
                            <span class="text-xs font-bold text-green-600 bg-green-50 px-2 py-1 rounded-full">عروض الأسعار</span>
                        </div>
                        <h3 class="text-3xl font-bold text-gray-800 mb-1" id="stats-total-quotes">0</h3>
                        <p class="text-xs text-gray-500">عرض سعر</p>
                    </div>
                    
                    <!-- 6. المبيعات -->
                    <div class="stats-card bg-white p-5 shadow-card hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-1 border border-gray-100">
                        <div class="flex items-center justify-between mb-4">
                            <div class="p-3 bg-gradient-to-br from-blue-500 to-blue-600 rounded-xl shadow-lg shadow-blue-500/30">
                                <i class="ri-line-chart-line text-2xl text-white"></i>
                            </div>
                            <span class="text-xs font-bold text-blue-600 bg-blue-50 px-2 py-1 rounded-full">المبيعات</span>
                        </div>
                        <h3 class="text-3xl font-bold text-gray-800 mb-1" id="stats-total-sales">0</h3>
                        <p class="text-xs text-gray-500">أمر بيع</p>
                    </div>
                    
                    <!-- 7. الشكاوى -->
                    <div class="stats-card bg-white p-5 shadow-card hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-1 border border-gray-100">
                        <div class="flex items-center justify-between mb-4">
                            <div class="p-3 bg-gradient-to-br from-orange-500 to-orange-600 rounded-xl shadow-lg shadow-orange-500/30">
                                <i class="ri-alert-line text-2xl text-white"></i>
                            </div>
                            <span class="text-xs font-bold text-orange-600 bg-orange-50 px-2 py-1 rounded-full">الشكاوى</span>
                        </div>
                        <h3 class="text-3xl font-bold text-gray-800 mb-1" id="stats-total-complaints">0</h3>
                        <p class="text-xs text-gray-500">شكوى مسجلة</p>
                    </div>
                    
                    <!-- 8. التحصيلات -->
                    <div class="stats-card bg-white p-5 shadow-card hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-1 border border-gray-100">
                        <div class="flex items-center justify-between mb-4">
                            <div class="p-3 bg-gradient-to-br from-amber-500 to-amber-600 rounded-xl shadow-lg shadow-amber-500/30">
                                <i class="ri-money-dollar-circle-line text-2xl text-white"></i>
                            </div>
                            <span class="text-xs font-bold text-amber-600 bg-amber-50 px-2 py-1 rounded-full">التحصيلات</span>
                        </div>
                        <h3 class="text-3xl font-bold text-gray-800 mb-1" id="stats-total-collections">0</h3>
                        <p class="text-xs text-gray-500">متابعة تحصيل</p>
                    </div>
                </div>

                <!-- صف خاص بالمسؤول فقط -->
                <div id="admin-only-row" class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8 hidden">
                    <!-- طلبات المستخدمين الجدد -->
                    <div id="pending-users-section" class="table-container overflow-hidden">
                        <div class="bg-gradient-to-r from-amber-500 to-amber-600 p-5 text-white">
                            <h2 class="text-xl font-bold flex items-center gap-3">
                                <i class="ri-user-add-line text-2xl"></i>
                                طلبات المستخدمين الجدد
                            </h2>
                        </div>
                        <div class="overflow-x-auto max-h-96 overflow-y-auto">
                            <table class="w-full">
                                <thead class="bg-gray-50 sticky top-0 z-10">
                                    <tr>
                                        <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">اسم المستخدم</th>
                                        <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">البريد الإلكتروني</th>
                                        <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">تاريخ الطلب</th>
                                        <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">الإجراءات</th>
                                    </tr>
                                </thead>
                                <tbody id="pending-users-table" class="divide-y divide-gray-100">
                                    <tr><td colspan="4" class="px-6 py-12 text-center text-gray-500">
                                        <div class="flex flex-col items-center gap-2">
                                            <i class="ri-loader-4-line text-3xl animate-spin text-primary"></i>
                                            <span>جاري التحميل...</span>
                                        </div>
                                    </td></tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                    
                    <!-- قائمة الموظفين -->
                    <div id="users-list-section" class="table-container overflow-hidden">
                        <div class="bg-gradient-to-r from-primary to-primaryDark p-5 text-white">
                            <h2 class="text-xl font-bold flex items-center gap-3">
                                <i class="ri-team-line text-2xl"></i>
                                قائمة الموظفين
                            </h2>
                        </div>
                        <div class="overflow-x-auto max-h-96 overflow-y-auto">
                            <table class="w-full">
                                <thead class="bg-gray-50 sticky top-0 z-10">
                                    <tr>
                                        <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">اسم المستخدم</th>
                                        <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">الدور</th>
                                        <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">الإجراءات</th>
                                    </tr>
                                </thead>
                                <tbody id="users-list" class="divide-y divide-gray-100">
                                    <tr><td colspan="3" class="px-6 py-12 text-center text-gray-500">
                                        <div class="flex flex-col items-center gap-2">
                                            <i class="ri-loader-4-line text-3xl animate-spin text-primary"></i>
                                            <span>جاري التحميل...</span>
                                        </div>
                                    </td></tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>

                <!-- سجل النشاطات -->
                <div class="table-container mb-8 overflow-hidden">
                    <div class="bg-gradient-to-r from-pink-500 via-purple-500 to-blue-500 p-5 text-white">
                        <h2 class="text-xl font-bold flex items-center gap-3">
                            <i class="ri-history-line text-2xl"></i>
                            سجل النشاطات
                        </h2>
                    </div>
                    <div class="overflow-x-auto">
                        <table class="w-full min-w-max">
                            <thead class="bg-gray-50 sticky top-0 z-10">
                                <tr>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b whitespace-nowrap">اسم الموظف</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b whitespace-nowrap">العملاء</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b whitespace-nowrap">الخطط</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b whitespace-nowrap">الزيارات</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b whitespace-nowrap">الأنشطة</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b whitespace-nowrap">عروض الأسعار</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b whitespace-nowrap">المبيعات</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b whitespace-nowrap">الشكاوى</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b whitespace-nowrap">التحصيلات</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b whitespace-nowrap">آخر نشاط</th>
                                 </tr>
                            </thead>
                            <tbody id="activities-log" class="divide-y divide-gray-100">
                                <tr><td colspan="10" class="px-6 py-12 text-center text-gray-500">لا توجد بيانات</td></tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- جدول العملاء -->
                <div class="table-container mb-8 overflow-hidden">
                    <div class="bg-gradient-to-r from-gray-600 to-purple-600 p-5 text-white flex flex-wrap justify-between items-center gap-4">
                        <h2 class="text-xl font-bold flex items-center gap-3">
                            <i class="ri-user-star-line text-2xl"></i>
                            العملاء
                        </h2>
                        <div class="flex gap-3">
                            <button type="button" onclick="approveSelectedCustomers()" class="bg-green-500 hover:bg-green-600 text-white px-5 py-2.5 rounded-xl text-sm font-bold shadow-lg shadow-green-500/30 transition-all flex items-center gap-2 hover:scale-105">
                                <i class="ri-check-double-line text-lg"></i>
                                <span>اعتماد المحدد</span>
                            </button>
                            <button type="button" onclick="rejectSelectedCustomers()" class="bg-red-500 hover:bg-red-600 text-white px-5 py-2.5 rounded-xl text-sm font-bold shadow-lg shadow-red-500/30 transition-all flex items-center gap-2 hover:scale-105">
                                <i class="ri-close-circle-line text-lg"></i>
                                <span>رفض المحدد</span>
                            </button>
                        </div>
                    </div>
                    <div class="overflow-x-auto max-h-[600px] overflow-y-auto">
                        <table class="w-full">
                            <thead class="bg-gray-50 sticky top-0 z-10 shadow-sm">
                                <tr>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b"><input type="checkbox" id="select-all-customers" onclick="toggleAllCustomers()" class="custom-checkbox"></th>
                                    <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">عرض</th>
                                    <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">م</th>
                                    <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">التاريخ</th>
                                    <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">الموظف</th>
                                    <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">اسم العميل</th>
                                    <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">الحالة</th>
                                    <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">ملاحظات</th>
                                    <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">المرفقات</th>
                                    <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">الإجراءات</th>

                                 </tr>
                            </thead>
                            <tbody id="admin-customers-table" class="divide-y divide-gray-100">
                                <!-- يتم ملؤه ديناميكياً -->
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- جدول النشاط اليومي -->
                <div class="table-container mb-8 overflow-hidden">
                    <div class="bg-gradient-to-r from-gray-600 to-teal-600 p-5 text-white flex justify-between items-center">
                        <h2 class="text-xl font-bold flex items-center gap-3">
                            <i class="ri-calendar-check-line text-2xl"></i>
                            النشاط اليومي
                        </h2>
                    </div>
                    <div class="overflow-x-auto max-h-[600px] overflow-y-auto">
                        <table class="w-full">
                            <thead class="bg-gray-50 sticky top-0 z-10 shadow-sm">
                                <tr>
                                    <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">عرض</th>
                                    <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">م</th>
                                    <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">التاريخ</th>
                                    <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">الموظف</th>
                                    <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">تفاصيل الأنشطة</th>
                                    <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">ملاحظات</th>
                                 </tr>
                            </thead>
                            <tbody id="admin-activities-table" class="divide-y divide-gray-100">
                                <tr><td colspan="6" class="px-6 py-12 text-center text-gray-500">
                                    <div class="flex flex-col items-center gap-2">
                                        <i class="ri-loader-4-line text-3xl animate-spin text-primary"></i>
                                        <span>جاري التحميل...</span>
                                    </div>
                                </td></tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- جدول زيارات العملاء -->
                <div class="table-container mb-8 overflow-hidden">
                    <div class="bg-gradient-to-r from-gray-600 to-indigo-600 p-5 text-white flex justify-between items-center">
                        <h2 class="text-xl font-bold flex items-center gap-3">
                            <i class="ri-user-location-line text-2xl"></i>
                            زيارات العملاء
                        </h2>
                    </div>
                    <div class="overflow-x-auto max-h-[600px] overflow-y-auto">
                        <table class="w-full">
                            <thead class="bg-gray-50 sticky top-0 z-10 shadow-sm">
                                <tr>
                                    <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">عرض</th>
                                    <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">م</th>
                                    <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">التاريخ</th>
                                    <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">الموظف</th>
                                    <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">العميل</th>
                                    <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">الموقع (GPS)</th>
                                    <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">وقت الدخول</th>
                                    <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">وقت الخروج</th>
                                    <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">الغرض</th>
                                    <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">النتيجة</th>
                                    <th class="px-6 py-4 text-right text-sm font-bold text-gray-700 border-b">ملاحظات</th>
                                 </tr>
                            </thead>
                            <tbody id="admin-visits-table" class="divide-y divide-gray-100">
                                <tr><td colspan="11" class="px-6 py-12 text-center text-gray-500">
                                    <div class="flex flex-col items-center gap-2">
                                        <i class="ri-loader-4-line text-3xl animate-spin text-primary"></i>
                                        <span>جاري التحميل...</span>
                                    </div>
                                </td></tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- عروض الأسعار -->
                <div class="table-container mb-8 overflow-hidden">
                    <div class="bg-gradient-to-r from-gray-600 to-green-600 p-5 text-white flex flex-wrap justify-between items-center gap-4">
                        <h2 class="text-xl font-bold flex items-center gap-3">
                            <i class="ri-file-list-line text-2xl"></i>
                            عروض الأسعار
                        </h2>
                        <div class="flex gap-3">
                            <button type="button" onclick="approveSelected('quote')" class="bg-green-500 hover:bg-green-600 text-white px-5 py-2.5 rounded-xl text-sm font-bold shadow-lg shadow-green-500/30 transition-all flex items-center gap-2 hover:scale-105">
                                <i class="ri-check-double-line text-lg"></i>
                                <span>اعتماد المحدد</span>
                            </button>
                            <button type="button" onclick="rejectSelected('quote')" class="bg-red-500 hover:bg-red-600 text-white px-5 py-2.5 rounded-xl text-sm font-bold shadow-lg shadow-red-500/30 transition-all flex items-center gap-2 hover:scale-105">
                                <i class="ri-close-circle-line text-lg"></i>
                                <span>رفض المحدد</span>
                            </button>
                        </div>
                    </div>
                    <div class="overflow-x-auto max-h-[600px] overflow-y-auto">
                        <table class="w-full">
                            <thead class="bg-gray-50 sticky top-0 z-10 shadow-sm">
                                <tr>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b"><input type="checkbox" id="select-all-quotes" onclick="toggleAll('quote')" class="custom-checkbox"></th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">عرض</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">التاريخ</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">الموظف</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">العميل</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">تفاصيل الأصناف</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">طريقة السداد</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">مكان التسليم</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">الحالة</th>
                                 </tr>
                            </thead>
                            <tbody id="admin-all-quotes-table" class="divide-y divide-gray-100">
                                <!-- يتم ملؤه ديناميكياً -->
                            </tbody>
                        </table>
                    </div>
                </div>
                
                <!-- تقارير المبيعات -->
                <div class="table-container mb-8 overflow-hidden">
                    <div class="bg-gradient-to-r from-gray-600 to-blue-600 p-5 text-white flex flex-wrap justify-between items-center gap-4">
                        <h2 class="text-xl font-bold flex items-center gap-3">
                            <i class="ri-line-chart-line text-2xl"></i>
                            تقارير المبيعات
                        </h2>
                        <div class="flex gap-3">
                            <button type="button" onclick="approveSelected('sale')" class="bg-green-500 hover:bg-green-600 text-white px-5 py-2.5 rounded-xl text-sm font-bold shadow-lg shadow-green-500/30 transition-all flex items-center gap-2 hover:scale-105">
                                <i class="ri-check-double-line text-lg"></i>
                                <span>اعتماد المحدد</span>
                            </button>
                            <button type="button" onclick="rejectSelected('sale')" class="bg-red-500 hover:bg-red-600 text-white px-5 py-2.5 rounded-xl text-sm font-bold shadow-lg shadow-red-500/30 transition-all flex items-center gap-2 hover:scale-105">
                                <i class="ri-close-circle-line text-lg"></i>
                                <span>رفض المحدد</span>
                            </button>
                        </div>
                    </div>
                    <div class="overflow-x-auto max-h-[600px] overflow-y-auto">
                        <table class="w-full">
                            <thead class="bg-gray-50 sticky top-0 z-10 shadow-sm">
                                <tr>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b"><input type="checkbox" id="select-all-sales" onclick="toggleAll('sale')" class="custom-checkbox"></th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">عرض</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">التاريخ</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">الموظف</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">العميل</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">تفاصيل الأصناف</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">مكان التصنيع</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">طريقة السداد</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">مكان التسليم</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">الحالة</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">ملاحظات</th>
                                 </tr>
                            </thead>
                            <tbody id="admin-all-sales-table" class="divide-y divide-gray-100">
                                <!-- يتم ملؤه ديناميكياً -->
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- جميع الشكاوى -->
                <div class="table-container overflow-hidden">
                    <div class="bg-gradient-to-r from-gray-600 to-orange-600 p-5 text-white flex flex-wrap justify-between items-center gap-4">
                        <h2 class="text-xl font-bold flex items-center gap-3">
                            <i class="ri-alert-line text-2xl"></i>
                            الشكاوى
                        </h2>
                        <div class="flex gap-3">
                            <button type="button" onclick="approveSelected('complaint')" class="bg-green-500 hover:bg-green-600 text-white px-5 py-2.5 rounded-xl text-sm font-bold shadow-lg shadow-green-500/30 transition-all flex items-center gap-2 hover:scale-105">
                                <i class="ri-check-double-line text-lg"></i>
                                <span>اعتماد المحدد</span>
                            </button>
                            <button type="button" onclick="rejectSelected('complaint')" class="bg-red-500 hover:bg-red-600 text-white px-5 py-2.5 rounded-xl text-sm font-bold shadow-lg shadow-red-500/30 transition-all flex items-center gap-2 hover:scale-105">
                                <i class="ri-close-circle-line text-lg"></i>
                                <span>رفض المحدد</span>
                            </button>
                        </div>
                    </div>
                    <div class="overflow-x-auto max-h-[600px] overflow-y-auto">
                        <table class="w-full">
                            <thead class="bg-gray-50 sticky top-0 z-10 shadow-sm">
                                <tr>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b"><input type="checkbox" id="select-all-complaints" onclick="toggleAll('complaint')" class="custom-checkbox"></th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">عرض</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">التاريخ</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">الموظف</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">العميل</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">رقم الهاتف</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">مسؤول التواصل</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">رقم مسؤول التواصل</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">طريقة الشكوى</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">النوع</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">الحالة</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">الوصف</th>
                                    <th class="px-4 py-4 text-right text-sm font-bold text-gray-700 border-b">المرفق</th>
                                 </tr>
                            </thead>
                            <tbody id="admin-all-complaints-table" class="divide-y divide-gray-100">
                                <!-- يتم ملؤه ديناميكياً -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </main>
    </div>

    
    <!-- مودال إدارة رسائل المسؤول -->
<div id="messages-modal" class="fixed inset-0 flex items-center justify-center z-50 modal-backdrop hidden">
    <div class="bg-white rounded-2xl p-6 w-full max-w-2xl mx-4 max-h-[85vh] overflow-y-auto shadow-2xl border border-gray-100 animate-slide-up">
        <div class="flex justify-between items-center mb-6 pb-4 border-b border-gray-100">
            <h3 class="text-xl font-bold text-gray-800 flex items-center gap-2">
                <i class="ri-message-3-line text-primary"></i>
                إدارة رسائل المسؤول
            </h3>
            <button onclick="closeMessagesModal()" class="text-gray-400 hover:text-gray-600 transition-colors p-2 hover:bg-gray-100 rounded-lg">
                <i class="ri-close-line text-2xl"></i>
            </button>
        </div>
        <p class="text-sm text-gray-500 mb-4 bg-gray-50 p-3 rounded-lg">أدخل الرسائل التي تريد عرضها في الشريط المتحرك للموظفين، كل رسالة في سطر منفصل.</p>
        <textarea id="admin-messages-textarea" rows="8" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus resize-none mb-5" placeholder="الرسالة الأولى&#10;الرسالة الثانية&#10;الرسالة الثالثة"></textarea>
        
        <div class="flex items-center gap-4 mb-6 bg-gray-50 p-4 rounded-xl">
            <label class="text-sm font-bold text-gray-700 whitespace-nowrap">سرعة الحركة (ثانية):</label>
            <input type="number" id="marquee-speed" min="5" max="100" value="25" class="w-24 px-3 py-2 border-2 border-gray-200 rounded-lg focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all">
            <button onclick="updateMarqueeSpeed()" class="bg-gray-200 hover:bg-gray-300 px-4 py-2 rounded-lg text-sm font-bold transition-all">تطبيق</button>
        </div>

        <div class="flex gap-3 pt-4 border-t border-gray-100">
            <button onclick="saveMessages()" class="flex-1 bg-gradient-to-r from-primary to-primaryDark text-white py-3.5 rounded-xl font-bold shadow-lg shadow-primary/30 hover:shadow-xl transition-all duration-300 btn-ripple flex items-center justify-center gap-2">
                <i class="ri-save-line text-lg"></i>
                <span>حفظ التغييرات</span>
            </button>
            <button onclick="closeMessagesModal()" class="flex-1 bg-gray-100 hover:bg-gray-200 text-gray-700 py-3.5 rounded-xl font-bold transition-all duration-300 flex items-center justify-center gap-2">
                <i class="ri-close-line text-lg"></i>
                <span>إلغاء</span>
            </button>
        </div>
    </div>
</div>

<!-- مودال رفع قائمة الأسعار -->
<div id="price-list-modal" class="fixed inset-0 flex items-center justify-center z-50 modal-backdrop hidden">
    <div class="bg-white rounded-2xl p-6 w-full max-w-md mx-4 shadow-2xl border border-gray-100 animate-slide-up">
        <div class="flex justify-between items-center mb-6 pb-4 border-b border-gray-100">
            <h3 class="text-xl font-bold text-gray-800 flex items-center gap-2">
                <i class="ri-price-tag-3-line text-red-500"></i>
                رفع قائمة الأسعار
            </h3>
            <button onclick="closePriceListModal()" class="text-gray-400 hover:text-gray-600 transition-colors p-2 hover:bg-gray-100 rounded-lg">
                <i class="ri-close-line text-2xl"></i>
            </button>
        </div>
        <form id="price-list-form" class="space-y-5">
            <div class="space-y-2">
                <label class="block text-sm font-bold text-gray-700">نوع المستند</label>
                <div class="relative">
                    <i class="ri-file-type-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400"></i>
                    <select id="price-list-type" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50 appearance-none">
                        <option value="image">صورة</option>
                        <option value="pdf">PDF</option>
                        <option value="word">Word</option>
                    </select>
                    <i class="ri-arrow-down-s-line absolute left-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg pointer-events-none"></i>
                </div>
            </div>
            <div class="space-y-2">
                <label class="block text-sm font-bold text-gray-700">الملف</label>
                <input type="file" id="price-list-file" accept=".jpg,.jpeg,.png,.pdf,.doc,.docx" class="file-input-primary w-full px-4 py-3 border-2 border-dashed border-gray-300 rounded-xl hover:border-primary transition-colors bg-gray-50/50" required>
            </div>
            <div class="flex gap-3 pt-4">
                <button type="button" onclick="uploadPriceList()" class="flex-1 bg-gradient-to-r from-primary to-primaryDark text-white py-3.5 rounded-xl font-bold shadow-lg shadow-primary/30 hover:shadow-xl transition-all duration-300 btn-ripple flex items-center justify-center gap-2">
                    <i class="ri-upload-cloud-2-line text-lg"></i>
                    <span>رفع</span>
                </button>
                <button type="button" onclick="closePriceListModal()" class="flex-1 bg-gray-100 hover:bg-gray-200 text-gray-700 py-3.5 rounded-xl font-bold transition-all duration-300 flex items-center justify-center gap-2">
                    <i class="ri-close-line text-lg"></i>
                    <span>إلغاء</span>
                </button>
            </div>
        </form>
        <div id="price-list-link-container" class="mt-5 p-4 bg-gray-50 rounded-xl hidden">
            <p class="text-sm text-gray-600 mb-2 font-bold">الرابط الحالي:</p>
            <a id="price-list-link" href="#" target="_blank" class="text-primary hover:text-primaryDark hover:underline break-all text-sm font-medium"></a>
        </div>
    </div>
</div>

<!-- ============================================== -->
<!--              User Page (Employee)              -->
<!-- ============================================== -->
<div id="user-page" class="hidden min-h-screen flex flex-col">
    <!-- Navbar -->
    <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
        <div class="max-w-7xl mx-auto px-4 py-3 flex justify-between items-center">
            <div class="flex items-center gap-4">
                <button onclick="showPage('user-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all">
                    <i class="ri-home-4-line text-xl"></i>
                </button>
                <div>
                    <h1 class="text-xl font-bold tracking-tight">Hyma Plastic</h1>
                    <span class="text-xs text-white/70">نظام إدارة المبيعات</span>
                </div>
            </div>
            <div class="flex items-center gap-4 relative">
                <div class="hidden md:flex flex-col items-end">
                    <span id="user-name" class="text-sm font-bold"></span>
                    <span id="user-role" class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm"></span>
                </div>
                
                <!-- Notifications Bell -->
                <div class="relative">
                    <button id="notif-bell" class="hover:bg-white/20 p-2.5 rounded-xl transition-all relative" onclick="toggleNotificationsPanel(event)">
                        <i class="ri-notification-3-line text-xl"></i>
                        <span id="notif-badge-count" class="notif-badge hidden">0</span>
                    </button>
                    <div id="notifications-dropdown" class="notifications-dropdown hidden w-80 max-h-96 overflow-y-auto">
                        <div class="p-3 bg-gray-50 dark:bg-gray-800 border-b font-bold text-gray-700 dark:text-gray-300">الإشعارات</div>
                        <div id="notifications-list" class="divide-y divide-gray-100 dark:divide-gray-700">
                            <div class="p-4 text-center text-gray-500">لا توجد إشعارات</div>
                        </div>
                        <button onclick="clearAllNotifications()" class="w-full text-center text-red-500 py-2 text-sm hover:bg-red-50 dark:hover:bg-red-900/20">مسح الكل</button>
                    </div>
                </div>
                
                <!-- Profile Dropdown -->
                <div class="relative">
                    <button id="profile-btn" class="hover:bg-white/20 p-2.5 rounded-xl transition-all flex items-center gap-2" onclick="toggleProfileDropdown(event)">
                        <i class="ri-user-settings-line text-xl"></i>
                        <i class="ri-arrow-down-s-line text-sm"></i>
                    </button>
                    <div id="profile-dropdown" class="profile-dropdown hidden">
                        <div class="px-4 py-3 border-b bg-gray-50 dark:bg-gray-800">
                            <div class="font-bold text-gray-800 dark:text-white" id="dropdown-username"></div>
                            <div class="text-xs text-gray-500" id="dropdown-role"></div>
                        </div>
                        <button onclick="showPage('profile-page'); closeProfileDropdown();">
                            <i class="ri-user-line"></i> الملف الشخصي
                        </button>
                        <button onclick="showReportsPage(); closeProfileDropdown();">
                            <i class="ri-file-list-line"></i> التقارير
                        </button>
                        <button onclick="logout(); closeProfileDropdown();">
                            <i class="ri-logout-box-r-line"></i> تسجيل الخروج
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </nav>

    <!-- Marquee Messages -->
    <div class="bg-gradient-to-r from-amber-500 to-orange-500 text-white py-3 fixed top-[72px] w-full z-40 shadow-lg">
        <div class="max-w-7xl mx-auto px-4 flex items-center gap-4">
            <div class="bg-red-600 px-4 py-1.5 rounded-lg text-sm font-bold whitespace-nowrap shadow-lg flex items-center gap-2">
                <i class="ri-notification-3-line animate-pulse"></i>
                <span>تعليمات هامة</span>
            </div>
            <div class="flex-1 marquee-container relative h-8 flex items-center">
                <div id="marquee-text" class="marquee-text text-sm md:text-base font-medium">
                    لا توجد رسائل
                </div>
            </div>
        </div>
    </div>

    <!-- Main Content -->
    <main class="flex-1 pt-36 pb-20 px-4">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-center mb-8">
                <div>
                    <h2 class="text-3xl font-bold text-gray-800 dark:text-white mb-1">أهلاً بك</h2>
                    <p class="text-gray-500 dark:text-gray-400 text-sm">اختر الخدمة المطلوبة من القائمة أدناه</p>
                </div>
                <button onclick="showPriceList()" class="bg-gradient-to-r from-red-500 to-red-600 hover:from-red-600 hover:to-red-700 text-white px-6 py-3 rounded-xl flex items-center gap-3 shadow-lg shadow-red-500/30 transition-all hover:scale-105 font-bold">
                    <i class="ri-price-tag-3-line text-xl"></i>
                    <span>قائمة الأسعار</span>
                </button>
            </div>

            <!-- Modern Cards Grid -->
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
                <!-- 1. تكويد عميل جديد -->
                <div class="modern-card rounded-2xl p-6 relative overflow-hidden group cursor-pointer" onclick="showPage('new-customer-page')">
                    <div class="absolute top-0 right-0 w-32 h-32 bg-gradient-to-br from-primary/10 to-transparent rounded-full -mr-10 -mt-10"></div>
                    <div class="relative z-10">
                        <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-primary to-primaryLight flex items-center justify-center mb-4 shadow-lg group-hover:scale-110 transition-transform">
                            <i class="ri-user-star-line text-2xl text-white"></i>
                        </div>
                        <h3 class="text-lg font-bold text-gray-800 dark:text-white mb-2">تكويد عميل جديد</h3>
                        <p class="text-sm text-gray-500 dark:text-gray-400 mb-4">إضافة عميل جديد للنظام</p>
                        <span class="inline-flex items-center text-primary text-sm font-semibold group-hover:gap-2 transition-all">
                            ابدأ الآن <i class="ri-arrow-left-line mr-1 group-hover:mr-2 transition-all"></i>
                        </span>
                    </div>
                </div>
                
                <!-- 2. الخطة الأسبوعية -->
                <div class="modern-card rounded-2xl p-6 relative overflow-hidden group cursor-pointer" onclick="showPage('weekly-plan-page')">
                    <div class="absolute top-0 right-0 w-32 h-32 bg-gradient-to-br from-cyan-500/10 to-transparent rounded-full -mr-10 -mt-10"></div>
                    <div class="relative z-10">
                        <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-cyan-500 to-cyan-600 flex items-center justify-center mb-4 shadow-lg group-hover:scale-110 transition-transform">
                            <i class="ri-calendar-todo-line text-2xl text-white"></i>
                        </div>
                        <h3 class="text-lg font-bold text-gray-800 dark:text-white mb-2">الخطة الأسبوعية</h3>
                        <p class="text-sm text-gray-500 dark:text-gray-400 mb-4">تخطيط المهام للأسبوع</p>
                        <span class="inline-flex items-center text-primary text-sm font-semibold group-hover:gap-2 transition-all">
                            ابدأ الآن <i class="ri-arrow-left-line mr-1 group-hover:mr-2 transition-all"></i>
                        </span>
                    </div>
                </div>
                
                <!-- 3. تقرير زيارة عميل -->
                <div class="modern-card rounded-2xl p-6 relative overflow-hidden group cursor-pointer" onclick="showPage('visit-report-page')">
                    <div class="absolute top-0 right-0 w-32 h-32 bg-gradient-to-br from-indigo-500/10 to-transparent rounded-full -mr-10 -mt-10"></div>
                    <div class="relative z-10">
                        <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-indigo-500 to-indigo-600 flex items-center justify-center mb-4 shadow-lg group-hover:scale-110 transition-transform">
                            <i class="ri-user-location-line text-2xl text-white"></i>
                        </div>
                        <h3 class="text-lg font-bold text-gray-800 dark:text-white mb-2">تقرير زيارة عميل</h3>
                        <p class="text-sm text-gray-500 dark:text-gray-400 mb-4">تسجيل زيارات العملاء</p>
                        <span class="inline-flex items-center text-primary text-sm font-semibold group-hover:gap-2 transition-all">
                            ابدأ الآن <i class="ri-arrow-left-line mr-1 group-hover:mr-2 transition-all"></i>
                        </span>
                    </div>
                </div>
                
                <!-- 4. تقرير النشاط اليومي -->
                <div class="modern-card rounded-2xl p-6 relative overflow-hidden group cursor-pointer" onclick="showPage('daily-activity-page')">
                    <div class="absolute top-0 right-0 w-32 h-32 bg-gradient-to-br from-teal-500/10 to-transparent rounded-full -mr-10 -mt-10"></div>
                    <div class="relative z-10">
                        <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-teal-500 to-teal-600 flex items-center justify-center mb-4 shadow-lg group-hover:scale-110 transition-transform">
                            <i class="ri-calendar-check-line text-2xl text-white"></i>
                        </div>
                        <h3 class="text-lg font-bold text-gray-800 dark:text-white mb-2">تقرير النشاط اليومي</h3>
                        <p class="text-sm text-gray-500 dark:text-gray-400 mb-4">تسجيل الأنشطة اليومية</p>
                        <span class="inline-flex items-center text-primary text-sm font-semibold group-hover:gap-2 transition-all">
                            ابدأ الآن <i class="ri-arrow-left-line mr-1 group-hover:mr-2 transition-all"></i>
                        </span>
                    </div>
                </div>
                
                <!-- 5. عروض الأسعار -->
                <div class="modern-card rounded-2xl p-6 relative overflow-hidden group cursor-pointer" onclick="showPage('quote-page')">
                    <div class="absolute top-0 right-0 w-32 h-32 bg-gradient-to-br from-green-500/10 to-transparent rounded-full -mr-10 -mt-10"></div>
                    <div class="relative z-10">
                        <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-green-500 to-green-600 flex items-center justify-center mb-4 shadow-lg group-hover:scale-110 transition-transform">
                            <i class="ri-file-list-line text-2xl text-white"></i>
                        </div>
                        <h3 class="text-lg font-bold text-gray-800 dark:text-white mb-2">طلب اصدار عرض سعر</h3>
                        <p class="text-sm text-gray-500 dark:text-gray-400 mb-4">إنشاء عروض أسعار للعملاء</p>
                        <span class="inline-flex items-center text-primary text-sm font-semibold group-hover:gap-2 transition-all">
                            ابدأ الآن <i class="ri-arrow-left-line mr-1 group-hover:mr-2 transition-all"></i>
                        </span>
                    </div>
                </div>
                
                <!-- 6. أوامر البيع -->
                <div class="modern-card rounded-2xl p-6 relative overflow-hidden group cursor-pointer" onclick="showPage('sales-page')">
                    <div class="absolute top-0 right-0 w-32 h-32 bg-gradient-to-br from-blue-500/10 to-transparent rounded-full -mr-10 -mt-10"></div>
                    <div class="relative z-10">
                        <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-blue-500 to-blue-600 flex items-center justify-center mb-4 shadow-lg group-hover:scale-110 transition-transform">
                            <i class="ri-line-chart-line text-2xl text-white"></i>
                        </div>
                        <h3 class="text-lg font-bold text-gray-800 dark:text-white mb-2">أمر بيع</h3>
                        <p class="text-sm text-gray-500 dark:text-gray-400 mb-4">تسجيل أوامر البيع</p>
                        <span class="inline-flex items-center text-primary text-sm font-semibold group-hover:gap-2 transition-all">
                            ابدأ الآن <i class="ri-arrow-left-line mr-1 group-hover:mr-2 transition-all"></i>
                        </span>
                    </div>
                </div>
                
                <!-- 7. شكاوى العملاء -->
                <div class="modern-card rounded-2xl p-6 relative overflow-hidden group cursor-pointer" onclick="showPage('complaints-page')">
                    <div class="absolute top-0 right-0 w-32 h-32 bg-gradient-to-br from-orange-500/10 to-transparent rounded-full -mr-10 -mt-10"></div>
                    <div class="relative z-10">
                        <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-orange-500 to-orange-600 flex items-center justify-center mb-4 shadow-lg group-hover:scale-110 transition-transform">
                            <i class="ri-alert-line text-2xl text-white"></i>
                        </div>
                        <h3 class="text-lg font-bold text-gray-800 dark:text-white mb-2">شكاوى العملاء</h3>
                        <p class="text-sm text-gray-500 dark:text-gray-400 mb-4">تسجيل شكاوى العملاء</p>
                        <span class="inline-flex items-center text-primary text-sm font-semibold group-hover:gap-2 transition-all">
                            ابدأ الآن <i class="ri-arrow-left-line mr-1 group-hover:mr-2 transition-all"></i>
                        </span>
                    </div>
                </div>
                
                <!-- 8. متابعة التحصيلات -->
                <div class="modern-card rounded-2xl p-6 relative overflow-hidden group cursor-pointer" onclick="showPage('collections-page')">
                    <div class="absolute top-0 right-0 w-32 h-32 bg-gradient-to-br from-amber-500/10 to-transparent rounded-full -mr-10 -mt-10"></div>
                    <div class="relative z-10">
                        <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-amber-500 to-amber-600 flex items-center justify-center mb-4 shadow-lg group-hover:scale-110 transition-transform">
                            <i class="ri-money-dollar-circle-line text-2xl text-white"></i>
                        </div>
                        <h3 class="text-lg font-bold text-gray-800 dark:text-white mb-2">متابعة التحصيلات</h3>
                        <p class="text-sm text-gray-500 dark:text-gray-400 mb-4">متابعة تحصيل المستحقات</p>
                        <span class="inline-flex items-center text-primary text-sm font-semibold group-hover:gap-2 transition-all">
                            ابدأ الآن <i class="ri-arrow-left-line mr-1 group-hover:mr-2 transition-all"></i>
                        </span>
                    </div>
                </div>
            </div>
        </div>
    </main>
</div>

<!-- ============================================== -->
<!--              Reports Page                      -->
<!-- ============================================== -->
<div id="reports-page" class="hidden min-h-screen flex flex-col">
    <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
        <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <button onclick="showPage('user-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all">
                    <i class="ri-home-4-line text-xl"></i>
                </button>
                <h1 class="text-2xl font-bold">التقارير الشاملة</h1>
            </div>
            <div class="flex items-center gap-4">
                <span id="reports-user-name" class="text-sm font-bold"></span>
                <button onclick="showPage('user-page')" class="bg-white/10 hover:bg-white/20 backdrop-blur-sm px-4 py-2 rounded-xl transition-all flex items-center gap-2">
                    <i class="ri-arrow-right-line"></i> <span>عودة</span>
                </button>
            </div>
        </div>
    </nav>
    
    <main class="flex-1 pt-28 pb-16 px-4">
        <div class="max-w-7xl mx-auto">
            <div class="bg-white dark:bg-gray-800 rounded-2xl shadow-card p-6 border border-gray-100 dark:border-gray-700 mb-6">
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <div>
                        <label class="block text-sm font-bold text-gray-700 dark:text-gray-300 mb-1">اسم العميل</label>
                        <input type="text" id="report-filter-client" class="w-full px-4 py-2 border rounded-xl focus:border-primary dark:bg-gray-900 dark:border-gray-700" placeholder="بحث باسم العميل">
                    </div>
                    <div>
                        <label class="block text-sm font-bold text-gray-700 dark:text-gray-300 mb-1">من تاريخ</label>
                        <input type="date" id="report-filter-date-from" class="w-full px-4 py-2 border rounded-xl dark:bg-gray-900 dark:border-gray-700">
                    </div>
                    <div>
                        <label class="block text-sm font-bold text-gray-700 dark:text-gray-300 mb-1">إلى تاريخ</label>
                        <input type="date" id="report-filter-date-to" class="w-full px-4 py-2 border rounded-xl dark:bg-gray-900 dark:border-gray-700">
                    </div>
                </div>
                <div class="flex justify-end mt-4 gap-3">
                    <button onclick="applyReportsFilter()" class="btn-modern text-white px-6 py-2 rounded-xl font-bold shadow">تصفية</button>
                    <button onclick="resetReportsFilter()" class="bg-gray-200 dark:bg-gray-700 text-gray-700 dark:text-gray-300 px-6 py-2 rounded-xl font-bold">إعادة ضبط</button>
                    <button onclick="exportFilteredReports()" class="bg-success text-white px-6 py-2 rounded-xl font-bold flex items-center gap-2"><i class="ri-file-excel-line"></i> تصدير Excel</button>
                </div>
            </div>
            
            <div class="table-container overflow-hidden">
                <div class="overflow-x-auto max-h-[600px] overflow-y-auto">
                    <table class="modern-table w-full min-w-[800px]">
                        <thead class="sticky top-0 z-10">
                            <tr>
                                <th class="px-4 py-3 text-center">النوع</th>
                                <th class="px-4 py-3 text-center">رقم المستند</th>
                                <th class="px-4 py-3 text-center">التاريخ</th>
                                <th class="px-4 py-3 text-center">العميل</th>
                                <th class="px-4 py-3 text-center">الموظف</th>
                                <th class="px-4 py-3 text-center">الحالة</th>
                                <th class="px-4 py-3 text-center">عرض</th>
                            </tr>
                        </thead>
                        <tbody id="reports-table-body" class="divide-y divide-gray-100 dark:divide-gray-700">
                            <tr><td colspan="7" class="text-center py-8 text-gray-500">لا توجد بيانات</td></tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </main>
</div>

<!-- ============================================== -->
<!--              Profile Page                      -->
<!-- ============================================== -->
<div id="profile-page" class="hidden min-h-screen flex flex-col">
    <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
        <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <button onclick="showPage('user-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all">
                    <i class="ri-home-4-line text-xl"></i>
                </button>
                <h1 class="text-2xl font-bold">Hyma Plastic</h1>
            </div>
            <div class="flex items-center gap-4">
                <span id="profile-user-name" class="text-sm font-bold"></span>
                <span id="profile-user-role" class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm"></span>
                <button onclick="showPage('user-page')" class="bg-white/10 hover:bg-white/20 backdrop-blur-sm px-4 py-2 rounded-xl transition-all border border-white/10 hover:border-white/30 flex items-center gap-2 text-sm font-medium">
                    <i class="ri-arrow-right-line"></i>
                    <span>عودة</span>
                </button>
            </div>
        </div>
    </nav>
    
    <main class="flex-1 pt-28 pb-16 px-4">
        <div class="max-w-2xl mx-auto">
            <div class="bg-white dark:bg-gray-800 rounded-2xl shadow-card p-8 border border-gray-100 dark:border-gray-700">
                <div class="flex items-center gap-4 mb-8 pb-6 border-b border-gray-100 dark:border-gray-700">
                    <div class="w-16 h-16 rounded-2xl bg-gradient-to-br from-primary/20 to-primary/10 flex items-center justify-center">
                        <i class="ri-user-settings-line text-3xl text-primary"></i>
                    </div>
                    <div>
                        <h2 class="text-2xl font-bold text-gray-800 dark:text-white">الملف الشخصي</h2>
                        <p class="text-gray-500 dark:text-gray-400 text-sm">تحديث بياناتك الشخصية</p>
                    </div>
                </div>
                
                <form id="profile-form" class="space-y-5">
                    <div class="space-y-2">
                        <label class="block text-sm font-bold text-gray-700 dark:text-gray-300">اسم المستخدم</label>
                        <div class="relative">
                            <i class="ri-user-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                            <input type="text" id="profile-username" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 dark:border-gray-700 dark:bg-gray-900 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all bg-gray-50/50" required>
                        </div>
                    </div>
                    <div class="space-y-2">
                        <label class="block text-sm font-bold text-gray-700 dark:text-gray-300">البريد الإلكتروني</label>
                        <div class="relative">
                            <i class="ri-mail-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                            <input type="email" id="profile-email" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 dark:border-gray-700 dark:bg-gray-900 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all bg-gray-50/50" required>
                        </div>
                    </div>
                    <div class="space-y-2">
                        <label class="block text-sm font-bold text-gray-700 dark:text-gray-300">كلمة المرور (اتركها فارغة إذا لم ترد التغيير)</label>
                        <div class="relative">
                            <i class="ri-lock-password-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                            <input type="password" id="profile-password" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 dark:border-gray-700 dark:bg-gray-900 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all bg-gray-50/50" placeholder="أدخل كلمة مرور جديدة">
                        </div>
                    </div>
                    <div class="space-y-2">
                        <label class="block text-sm font-bold text-gray-700 dark:text-gray-300">تأكيد كلمة المرور</label>
                        <div class="relative">
                            <i class="ri-lock-password-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                            <input type="password" id="profile-confirm-password" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 dark:border-gray-700 dark:bg-gray-900 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all bg-gray-50/50" placeholder="أعد إدخال كلمة المرور الجديدة">
                        </div>
                    </div>
                    <div class="flex gap-3 pt-6 border-t border-gray-100 dark:border-gray-700">
                        <button type="submit" class="flex-1 btn-modern text-white py-3.5 rounded-xl font-bold shadow-lg hover:shadow-xl transition-all duration-300 flex items-center justify-center gap-2">
                            <i class="ri-save-line text-lg"></i>
                            <span>حفظ التغييرات</span>
                        </button>
                        <button type="button" onclick="showPage('user-page')" class="flex-1 bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 text-gray-700 dark:text-gray-300 py-3.5 rounded-xl font-bold transition-all duration-300 flex items-center justify-center gap-2">
                            <i class="ri-close-line text-lg"></i>
                            <span>إلغاء</span>
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </main>
</div>

 <!-- 1. تكويد عميل جديد -->
    <div id="new-customer-page" class="min-h-screen flex flex-col hidden page-transition bg-gradient-to-br from-gray-50 to-slate-100">
        <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
            <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
                <div class="flex items-center gap-3">
                    <button type="button" onclick="showPage('user-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الصفحة الرئيسية">
                        <i class="ri-home-4-line text-xl"></i>
                    </button>
                    <h1 class="text-2xl font-bold">Hyma Plastic</h1>
                </div>
                <div class="flex items-center gap-4">
                    <span id="customer-page-username" class="text-sm font-bold hidden md:inline"></span>
                    <span class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm" id="customer-page-role"></span>
                    <button type="button" onclick="showPage('profile-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الملف الشخصي">
                        <i class="ri-user-settings-line text-xl"></i>
                    </button>
                </div>
            </div>
        </nav>
        <main class="flex-1 pt-28 pb-16 px-4">
            <div class="max-w-7xl mx-auto">
                <div class="flex flex-wrap justify-between items-center mb-6 gap-4">
                    <h2 class="text-2xl font-bold text-gray-800 flex items-center gap-3">
                        <i class="ri-user-star-line text-primary text-3xl"></i>
                        قائمة العملاء المسجلين
                    </h2>
                    <div class="flex gap-3">
                        <button type="button" id="add-customer-btn" class="bg-gradient-to-r from-primary to-primaryDark text-white px-5 py-2.5 rounded-xl text-sm font-bold shadow-lg shadow-primary/30 transition-all flex items-center gap-2 hover:scale-105">
                            <i class="ri-add-line text-lg"></i>
                            <span>إضافة عميل</span>
                        </button>
                    </div>
                </div>
                <div class="table-container overflow-hidden">
                    <div class="overflow-x-auto max-h-[600px] overflow-y-auto">
                        <table class="w-full">
                            <thead class="bg-gray-50 sticky top-0 z-10 shadow-sm">
                                <tr>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">عرض</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">م</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">التاريخ</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">اسم العميل</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">نوع العميل</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">الحالة</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">ملاحظات</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">المرفقات</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">الإجراءات</th>
                                 </tr>
                            </thead>
                            <tbody id="my-customers-table" class="divide-y divide-gray-100">
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <!-- استبدل صفحة إضافة عميل (add-customer-page) بالكود التالي -->

<!-- صفحة إضافة عميل (معدلة) -->
<div id="add-customer-page" class="min-h-screen flex flex-col hidden page-transition bg-gradient-to-br from-gray-50 to-slate-100">
    <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
        <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <button type="button" onclick="showPage('new-customer-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الصفحة الرئيسية">
                    <i class="ri-home-4-line text-xl"></i>
                </button>
                <h1 class="text-2xl font-bold">Hyma Plastic</h1>
            </div>
            <div class="flex items-center gap-4">
                <span class="text-sm font-bold" id="add-customer-username"></span>
                <span class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm" id="add-customer-role"></span>
                <button type="button" onclick="showPage('profile-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الملف الشخصي">
                    <i class="ri-user-settings-line text-xl"></i>
                </button>
            </div>
        </div>
    </nav>
    <main class="flex-1 pt-28 pb-16 px-4">
        <div class="max-w-4xl mx-auto">
            <div class="bg-white rounded-2xl shadow-card p-8 border border-gray-100">
                <div class="flex items-center gap-4 mb-8 pb-6 border-b border-gray-100">
                    <div class="w-16 h-16 rounded-2xl bg-gradient-to-br from-purple-100 to-purple-200 flex items-center justify-center">
                        <i class="ri-user-add-line text-3xl text-purple-600"></i>
                    </div>
                    <div>
                        <h2 class="text-2xl font-bold text-gray-800">إضافة عميل جديد</h2>
                        <p class="text-gray-500 text-sm">أدخل بيانات العميل بشكل صحيح</p>
                    </div>
                </div>
                <form id="customer-form" class="space-y-6">
                    <input type="hidden" id="customer-id">
                    
                    <!-- الصف الأول: اسم العميل ونوع العميل -->
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">اسم العميل <span class="text-red-500">*</span></label>
                            <div class="relative">
                                <i class="ri-user-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <input type="text" id="customer-name" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50" required>
                            </div>
                        </div>
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">نوع العميل <span class="text-red-500">*</span></label>
                            <div class="relative">
                                <i class="ri-group-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <select id="customer-type" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50" required>
                                    <option value="">-- اختر نوع العميل --</option>
                                    <option value="شركة">شركة</option>
                                    <option value="شخص">شخص</option>
                                    <option value="عميل خارجي">عميل خارجي</option>
                                </select>
                            </div>
                        </div>
                    </div>

                    <!-- الصف الثاني: رقم الهاتف والبريد الإلكتروني -->
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">رقم الهاتف <span class="text-red-500">*</span></label>
                            <div class="relative">
                                <i class="ri-phone-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <input type="tel" id="customer-phone" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50" required>
                            </div>
                        </div>
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">البريد الإلكتروني</label>
                            <div class="relative">
                                <i class="ri-mail-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <input type="email" id="customer-email" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50">
                            </div>
                        </div>
                    </div>

                    <!-- الصف الثالث: مسؤول العميل وهاتف مسؤول العميل -->
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">مسؤول العميل</label>
                            <div class="relative">
                                <i class="ri-user-star-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <input type="text" id="customer-contact-person" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50" placeholder="اسم جهة الاتصال المسؤولة">
                            </div>
                        </div>
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">رقم هاتف مسؤول العميل</label>
                            <div class="relative">
                                <i class="ri-phone-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <input type="tel" id="customer-contact-phone" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50" placeholder="رقم هاتف جهة الاتصال">
                            </div>
                        </div>
                    </div>

                    <!-- الصف الرابع: حقول البطاقات (تظهر وتختفي ديناميكياً) -->
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <!-- حقل البطاقة الضريبية - يظهر فقط للشركات -->
                        <div class="space-y-2" id="tax-card-field" style="display: none;">
                            <label class="block text-sm font-bold text-gray-700">رقم البطاقة الضريبية</label>
                            <div class="relative">
                                <i class="ri-file-copy-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <input type="text" id="customer-tax-card" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50" placeholder="رقم السجل الضريبي">
                            </div>
                        </div>
                        
                        <!-- حقل البطاقة الشخصية - يظهر فقط للأشخاص -->
                        <div class="space-y-2" id="id-card-field" style="display: none;">
                            <label class="block text-sm font-bold text-gray-700">رقم البطاقة الشخصية</label>
                            <div class="relative">
                                <i class="ri-id-card-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <input type="text" id="customer-id-card" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50" placeholder="الرقم القومي">
                            </div>
                        </div>
                        
                        <!-- حقل الباسبور - يظهر فقط للعملاء الخارجيين -->
                        <div class="space-y-2" id="passport-field" style="display: none;">
                            <label class="block text-sm font-bold text-gray-700">رقم الباسبور</label>
                            <div class="relative">
                                <i class="ri-passport-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <input type="text" id="customer-passport" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50" placeholder="رقم جواز السفر">
                            </div>
                        </div>
                    </div>

                    <!-- الصف الخامس: العنوان -->
                    <div class="space-y-2">
                        <label class="block text-sm font-bold text-gray-700">العنوان</label>
                        <div class="relative">
                            <i class="ri-map-pin-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                            <input type="text" id="customer-address" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50">
                        </div>
                    </div>

                    <!-- الصف السادس: ملاحظات -->
                    <div class="space-y-2">
                        <label class="block text-sm font-bold text-gray-700">ملاحظات</label>
                        <textarea id="customer-notes" rows="4" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50 resize-none"></textarea>
                    </div>

                    <!-- الصف السابع: المرفقات -->
                    <div class="space-y-2">
                        <label class="block text-sm font-bold text-gray-700">المرفقات (صور، مستندات)</label>
                        <div class="relative">
                            <input type="file" id="customer-attachments" multiple class="file-input-primary w-full px-4 py-3 border-2 border-dashed border-gray-300 rounded-xl hover:border-primary transition-colors bg-gray-50/50" accept=".jpg,.jpeg,.png,.pdf,.doc,.docx" capture="environment">
                        </div>
                        <p class="text-xs text-gray-500 mt-1">يمكنك رفع عدة ملفات (صور، PDF، Word)</p>
                    </div>

                    <div class="flex justify-end pt-4 border-t border-gray-100">
                        <button type="submit" id="save-customer-btn" class="bg-gradient-to-r from-primary to-primaryDark text-white px-8 py-3.5 rounded-xl font-bold shadow-lg shadow-primary/30 hover:shadow-xl transition-all duration-300 btn-ripple flex items-center gap-2">
                            <i class="ri-save-line text-lg"></i>
                            <span>حفظ العميل</span>
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </main>
</div>

    <!-- 2. الخطة الأسبوعية -->
    <div id="weekly-plan-page" class="min-h-screen flex flex-col hidden page-transition bg-gradient-to-br from-gray-50 to-slate-100">
        <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
            <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
                <div class="flex items-center gap-3">
                    <button type="button" onclick="showPage('user-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الصفحة الرئيسية">
                        <i class="ri-home-4-line text-xl"></i>
                    </button>
                    <h1 class="text-2xl font-bold">Hyma Plastic</h1>
                </div>
                <div class="flex items-center gap-4">
                    <span class="text-sm font-bold" id="plan-page-username"></span>
                    <span class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm" id="plan-page-role"></span>
                    <button type="button" onclick="showPage('profile-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الملف الشخصي">
                        <i class="ri-user-settings-line text-xl"></i>
                    </button>
                </div>
            </div>
        </nav>
        <main class="flex-1 pt-28 pb-16 px-4">
            <div class="max-w-7xl mx-auto">
                <div class="flex flex-wrap justify-between items-center mb-6 gap-4">
                    <h2 class="text-2xl font-bold text-gray-800 flex items-center gap-3">
                        <i class="ri-calendar-todo-line text-cyan-600 text-3xl"></i>
                        الخطة الأسبوعية
                    </h2>
                    <div class="flex gap-3">
                        <button type="button" id="add-plan-btn" class="bg-gradient-to-r from-cyan-500 to-cyan-600 text-white px-5 py-2.5 rounded-xl text-sm font-bold shadow-lg shadow-cyan-500/30 transition-all flex items-center gap-2 hover:scale-105">
                            <i class="ri-add-line text-lg"></i>
                            <span>إضافة خطة</span>
                        </button>
                    </div>
                </div>
                <div class="table-container overflow-hidden">
                    <div class="overflow-x-auto max-h-[600px] overflow-y-auto">
                        <table class="w-full">
                            <thead class="bg-gray-50 sticky top-0 z-10 shadow-sm">
                                <tr>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">عرض</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">م</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">من تاريخ</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">إلى تاريخ</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">الأهداف</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">المهام</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">ملاحظات</th>
                                 </tr>
                            </thead>
                            <tbody id="my-plans-table" class="divide-y divide-gray-100">
                                <tr><td colspan="7" class="px-6 py-12 text-center text-gray-500">لا توجد بيانات</td></tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <!-- صفحة إضافة خطة -->
    <div id="add-plan-page" class="min-h-screen flex flex-col hidden page-transition bg-gradient-to-br from-gray-50 to-slate-100">
        <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
            <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
                <div class="flex items-center gap-3">
                    <button type="button" onclick="showPage('weekly-plan-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الصفحة الرئيسية">
                        <i class="ri-home-4-line text-xl"></i>
                    </button>
                    <h1 class="text-2xl font-bold">Hyma Plastic</h1>
                </div>
                <div class="flex items-center gap-4">
                    <span class="text-sm font-bold" id="add-plan-username"></span>
                    <span class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm" id="add-plan-role"></span>
                    <button type="button" onclick="showPage('profile-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الملف الشخصي">
                        <i class="ri-user-settings-line text-xl"></i>
                    </button>
                </div>
            </div>
        </nav>
        <main class="flex-1 pt-28 pb-16 px-4">
            <div class="max-w-4xl mx-auto">
                <div class="bg-white rounded-2xl shadow-card p-8 border border-gray-100">
                    <div class="flex items-center gap-4 mb-8 pb-6 border-b border-gray-100">
                        <div class="w-16 h-16 rounded-2xl bg-gradient-to-br from-cyan-100 to-cyan-200 flex items-center justify-center">
                            <i class="ri-calendar-add-line text-3xl text-cyan-600"></i>
                        </div>
                        <div>
                            <h2 class="text-2xl font-bold text-gray-800">الخطة الأسبوعية</h2>
                            <p class="text-gray-500 text-sm">حدد أهدافك ومهامك للأسبوع</p>
                        </div>
                    </div>
                    <form id="plan-form" class="space-y-6">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <div class="space-y-2">
                                <label class="block text-sm font-bold text-gray-700">من تاريخ <span class="text-red-500">*</span></label>
                                <div class="relative">
                                    <i class="ri-calendar-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                    <input type="date" id="plan-from" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50" required>
                                </div>
                            </div>
                            <div class="space-y-2">
                                <label class="block text-sm font-bold text-gray-700">إلى تاريخ <span class="text-red-500">*</span></label>
                                <div class="relative">
                                    <i class="ri-calendar-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                    <input type="date" id="plan-to" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50" required>
                                </div>
                            </div>
                        </div>
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">الأهداف</label>
                            <textarea id="plan-goals" rows="4" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50 resize-none" placeholder="اكتب أهدافك للأسبوع..."></textarea>
                        </div>
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">المهام</label>
                            <textarea id="plan-tasks" rows="4" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50 resize-none" placeholder="اكتب مهامك المطلوبة..."></textarea>
                        </div>
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">ملاحظات</label>
                            <textarea id="plan-notes" rows="3" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50 resize-none"></textarea>
                        </div>
                        <div class="flex justify-end pt-4 border-t border-gray-100">
                            <button type="submit" id="save-plan-btn" class="bg-gradient-to-r from-cyan-500 to-cyan-600 text-white px-8 py-3.5 rounded-xl font-bold shadow-lg shadow-cyan-500/30 hover:shadow-xl transition-all duration-300 btn-ripple flex items-center gap-2">
                                <i class="ri-save-line text-lg"></i>
                                <span>حفظ الخطة</span>
                            </button>
                        </div>
                    </form>
                </div>
            </div>
        </main>
    </div>

    <!-- 3. تقرير زيارة عميل -->
    <div id="visit-report-page" class="min-h-screen flex flex-col hidden page-transition bg-gradient-to-br from-gray-50 to-slate-100">
        <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
            <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
                <div class="flex items-center gap-3">
                    <button type="button" onclick="showPage('user-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الصفحة الرئيسية">
                        <i class="ri-home-4-line text-xl"></i>
                    </button>
                    <h1 class="text-2xl font-bold">Hyma Plastic</h1>
                </div>
                <div class="flex items-center gap-4">
                    <span class="text-sm font-bold" id="visit-page-username"></span>
                    <span class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm" id="visit-page-role"></span>
                    <button type="button" onclick="showPage('profile-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الملف الشخصي">
                        <i class="ri-user-settings-line text-xl"></i>
                    </button>
                </div>
            </div>
        </nav>
        <main class="flex-1 pt-28 pb-16 px-4">
            <div class="max-w-7xl mx-auto">
                <div class="flex flex-wrap justify-between items-center mb-6 gap-4">
                    <h2 class="text-2xl font-bold text-gray-800 flex items-center gap-3">
                        <i class="ri-user-location-line text-indigo-600 text-3xl"></i>
                        تقارير الزيارات
                    </h2>
                    <div class="flex gap-3">
                        <button type="button" id="add-visit-btn" class="bg-gradient-to-r from-indigo-500 to-indigo-600 text-white px-5 py-2.5 rounded-xl text-sm font-bold shadow-lg shadow-indigo-500/30 transition-all flex items-center gap-2 hover:scale-105">
                            <i class="ri-add-line text-lg"></i>
                            <span>إضافة زيارة</span>
                        </button>
                    </div>
                </div>
                <div class="table-container overflow-hidden">
                    <div class="overflow-x-auto max-h-[600px] overflow-y-auto">
                        <table class="w-full">
                            <thead class="bg-gray-50 sticky top-0 z-10 shadow-sm">
                                <tr>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">عرض</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">م</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">التاريخ</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">العميل</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">الموقع (GPS)</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">وقت الدخول</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">وقت الخروج</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">الغرض</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">النتيجة</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">ملاحظات</th>
                                 </tr>
                            </thead>
                            <tbody id="my-visits-table" class="divide-y divide-gray-100">
                                <tr><td colspan="10" class="px-6 py-12 text-center text-gray-500">لا توجد بيانات</td></tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <!-- صفحة إضافة زيارة -->
    <div id="add-visit-page" class="min-h-screen flex flex-col hidden page-transition bg-gradient-to-br from-gray-50 to-slate-100">
        <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
            <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
                <div class="flex items-center gap-3">
                    <button type="button" onclick="showPage('visit-report-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الصفحة الرئيسية">
                        <i class="ri-home-4-line text-xl"></i>
                    </button>
                    <h1 class="text-2xl font-bold">Hyma Plastic</h1>
                </div>
                <div class="flex items-center gap-4">
                    <span class="text-sm font-bold" id="add-visit-username"></span>
                    <span class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm" id="add-visit-role"></span>
                    <button type="button" onclick="showPage('profile-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الملف الشخصي">
                        <i class="ri-user-settings-line text-xl"></i>
                    </button>
                </div>
            </div>
        </nav>
        <main class="flex-1 pt-28 pb-16 px-4">
            <div class="max-w-4xl mx-auto">
                <div class="bg-white rounded-2xl shadow-card p-8 border border-gray-100">
                    <div class="flex items-center gap-4 mb-8 pb-6 border-b border-gray-100">
                        <div class="w-16 h-16 rounded-2xl bg-gradient-to-br from-indigo-100 to-indigo-200 flex items-center justify-center">
                            <i class="ri-map-pin-add-line text-3xl text-indigo-600"></i>
                        </div>
                        <div>
                            <h2 class="text-2xl font-bold text-gray-800">تقرير زيارة عميل</h2>
                            <p class="text-gray-500 text-sm">سجل تفاصيل زيارتك للعميل</p>
                        </div>
                    </div>
                    <form id="visit-form" class="space-y-6">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <div class="space-y-2">
                                <label class="block text-sm font-bold text-gray-700">التاريخ <span class="text-red-500">*</span></label>
                                <div class="relative">
                                    <i class="ri-calendar-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                    <input type="date" id="visit-date" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50" required>
                                </div>
                            </div>
                            <div class="space-y-2">
                                <label class="block text-sm font-bold text-gray-700">اختر عميلاً</label>
                                <select id="visit-client-select" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50">
                                    <option value="">-- اختر عميلاً --</option>
                                </select>
                            </div>
                        </div>

                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <div class="space-y-2">
                                <label class="block text-sm font-bold text-gray-700">وقت الدخول</label>
                                <div class="relative">
                                    <input type="time" id="visit-checkin" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50 text-left" dir="ltr">
                                    <i class="ri-time-line absolute left-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                </div>
                            </div>
                            <div class="space-y-2">
                                <label class="block text-sm font-bold text-gray-700">وقت الخروج</label>
                                <div class="relative">
                                    <input type="time" id="visit-checkout" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50 text-left" dir="ltr">
                                    <i class="ri-time-line absolute left-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                </div>
                            </div>
                        </div>

                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">الموقع (GPS)</label>
                            <div class="flex gap-3">
                                <div class="relative flex-1">
                                    <i class="ri-map-pin-2-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                    <input type="text" id="visit-location" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50" placeholder="انتظر يتم جلب الموقع..." readonly>
                                </div>
                                <button type="button" id="get-location-btn" class="bg-gradient-to-r from-primary to-primaryDark text-white px-6 py-3.5 rounded-xl font-bold shadow-lg shadow-primary/30 hover:shadow-xl transition-all duration-300 flex items-center gap-2 whitespace-nowrap">
                                    <i class="ri-gps-line text-lg"></i>
                                    <span>تحديث الموقع</span>
                                </button>
                            </div>
                        </div>

                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">الغرض من الزيارة</label>
                            <div class="relative">
                                <i class="ri-focus-3-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <select id="visit-purpose" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50 appearance-none">
                                    <option value="">اختر الغرض</option>
                                    <option value="مقابلة">مقابلة</option>
                                    <option value="متابعة">متابعة</option>
                                    <option value="تسويق">تسويق</option>
                                    <option value="شكوى">شكوى</option>
                                    <option value="تحصيل">تحصيل</option>
                                    <option value="أخرى">أخرى</option>
                                </select>
                                <i class="ri-arrow-down-s-line absolute left-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg pointer-events-none"></i>
                            </div>
                        </div>

                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">نتيجة الزيارة</label>
                            <textarea id="visit-result" rows="4" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50 resize-none" placeholder="اكتب نتيجة الزيارة..."></textarea>
                        </div>

                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">ملاحظات</label>
                            <textarea id="visit-notes" rows="3" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50 resize-none"></textarea>
                        </div>
                        <div class="flex justify-end pt-4 border-t border-gray-100">
                            <button type="submit" id="save-visit-btn" class="bg-gradient-to-r from-indigo-500 to-indigo-600 text-white px-8 py-3.5 rounded-xl font-bold shadow-lg shadow-indigo-500/30 hover:shadow-xl transition-all duration-300 btn-ripple flex items-center gap-2">
                                <i class="ri-save-line text-lg"></i>
                                <span>حفظ الزيارة</span>
                            </button>
                        </div>
                    </form>
                </div>
            </div>
        </main>
    </div>

    <!-- 4. النشاط اليومي -->
    <div id="daily-activity-page" class="min-h-screen flex flex-col hidden page-transition bg-gradient-to-br from-gray-50 to-slate-100">
        <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
            <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
                <div class="flex items-center gap-3">
                    <button type="button" onclick="showPage('user-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الصفحة الرئيسية">
                        <i class="ri-home-4-line text-xl"></i>
                    </button>
                    <h1 class="text-2xl font-bold">Hyma Plastic</h1>
                </div>
                <div class="flex items-center gap-4">
                    <span class="text-sm font-bold" id="activity-page-username"></span>
                    <span class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm" id="activity-page-role"></span>
                    <button type="button" onclick="showPage('profile-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الملف الشخصي">
                        <i class="ri-user-settings-line text-xl"></i>
                    </button>
                </div>
            </div>
        </nav>
        <main class="flex-1 pt-28 pb-16 px-4">
            <div class="max-w-7xl mx-auto">
                <div class="bg-white rounded-2xl shadow-card p-8 border border-gray-100">
                    <div class="flex flex-wrap justify-between items-center mb-6 gap-4">
                        <h2 class="text-2xl font-bold text-gray-800 flex items-center gap-3">
                            <i class="ri-calendar-check-line text-teal-600 text-3xl"></i>
                            النشاط اليومي
                        </h2>
                        <div class="flex gap-3">
                            <button type="button" id="add-activity-btn" class="bg-gradient-to-r from-teal-500 to-teal-600 text-white px-5 py-2.5 rounded-xl text-sm font-bold shadow-lg shadow-teal-500/30 transition-all flex items-center gap-2 hover:scale-105">
                                <i class="ri-add-line text-lg"></i>
                                <span>إضافة نشاط</span>
                            </button>
                        </div>
                    </div>
                    <div class="table-container overflow-hidden">
                        <div class="overflow-x-auto max-h-[600px] overflow-y-auto">
                            <table class="w-full">
                                <thead class="bg-gray-50 sticky top-0 z-10 shadow-sm">
                                    <tr>
                                        <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">عرض</th>
                                        <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">م</th>
                                        <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">التاريخ</th>
                                        <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">تفاصيل الأنشطة</th>
                                        <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">ملاحظات</th>
                                     </tr>
                                </thead>
                                <tbody id="my-activities-table" class="divide-y divide-gray-100">
                                    <tr><td colspan="5" class="px-6 py-12 text-center text-gray-500">لا توجد بيانات</td></tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <!-- صفحة إضافة نشاط يومي -->
<div id="add-activity-page" class="min-h-screen flex flex-col hidden page-transition bg-gradient-to-br from-gray-50 to-slate-100">
    <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
        <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <button type="button" onclick="showPage('daily-activity-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الصفحة الرئيسية">
                    <i class="ri-home-4-line text-xl"></i>
                </button>
                <h1 class="text-2xl font-bold">Hyma Plastic</h1>
            </div>
            <div class="flex items-center gap-4">
                <span class="text-sm font-bold" id="add-activity-username"></span>
                <span class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm" id="add-activity-role"></span>
                <button type="button" onclick="showPage('profile-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الملف الشخصي">
                    <i class="ri-user-settings-line text-xl"></i>
                </button>
            </div>
        </div>
    </nav>
    <main class="flex-1 pt-28 pb-16 px-4">
        <div class="max-w-6xl mx-auto">
            <div class="bg-white rounded-2xl shadow-card p-8 border border-gray-100">
                <div class="flex items-center gap-4 mb-8 pb-6 border-b border-gray-100">
                    <div class="w-16 h-16 rounded-2xl bg-gradient-to-br from-teal-100 to-teal-200 flex items-center justify-center">
                        <i class="ri-calendar-add-line text-3xl text-teal-600"></i>
                    </div>
                    <div>
                        <h2 class="text-2xl font-bold text-gray-800">تقرير النشاط اليومي</h2>
                        <p class="text-gray-500 text-sm">سجل أنشطتك اليومية مع العملاء</p>
                    </div>
                </div>

                <form id="activity-form" class="space-y-6">
                    <div class="space-y-2">
                        <label class="block text-sm font-bold text-gray-700">التاريخ <span class="text-red-500">*</span></label>
                        <div class="relative">
                            <i class="ri-calendar-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                            <input type="date" id="activity-date" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-100" readonly required>
                        </div>
                    </div>

                    <!-- زر مبني على (تم الاحتفاظ به) -->
                    <div class="mt-4 flex justify-end">
    <button type="button" id="based-on-docs-btn" onclick="openBasedOnModal()" class="bg-gradient-to-r from-amber-500 to-amber-600 text-white px-6 py-2.5 rounded-xl text-sm font-bold shadow-lg shadow-amber-500/30 transition-all flex items-center gap-2 hover:scale-105">
        <i class="ri-stackshare-line text-lg"></i>
        <span>مبني على</span>
    </button>
</div>

                    <!-- ⭐ جدول تفاصيل الأنشطة (تم إعادته) -->
                    <div class="space-y-3">
                        <label class="block text-sm font-bold text-gray-700">تفاصيل النشاطات</label>
                        <div class="overflow-x-auto rounded-xl border border-gray-200">
                            <table class="dynamic-table w-full" id="activities-detail-table" style="table-layout: fixed;">
                                <thead>
                                    <tr class="bg-gray-50">
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700 text-center border-b" style="width: 3%;">#</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700 text-right border-b" style="width: 14%;">اسم العميل / المسؤول</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700 text-right border-b" style="width: 11%;">العنوان</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700 text-center border-b" style="width: 9%;">الهاتف</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700 text-right border-b" style="width: 14%;">الموضوع</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700 text-right border-b" style="width: 14%;">ما تم</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700 text-center border-b" style="width: 8%;">مبيعات اليوم</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700 text-center border-b" style="width: 8%;">تحصيل اليوم</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700 text-center border-b" style="width: 7%;">من وقت</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700 text-center border-b" style="width: 7%;">إلى وقت</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700 text-center border-b" style="width: 5%;">الإجراءات</th>
                                    </tr>
                                </thead>
                                <tbody id="activities-detail-body"></tbody>
                            </table>
                        </div>
                    </div>

                    <!-- ملخص الإجماليات -->
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mt-4">
                        <div class="bg-gradient-to-r from-blue-50 to-blue-100 rounded-xl p-4 border border-blue-200">
                            <div class="flex items-center justify-between">
                                <span class="font-bold text-blue-800 text-lg">💰 إجمالي مبيعات اليوم:</span>
                                <span id="total-sales-today" class="font-bold text-blue-800 text-2xl">0</span>
                                <span class="font-bold text-blue-800">ج.م</span>
                            </div>
                        </div>
                        <div class="bg-gradient-to-r from-green-50 to-green-100 rounded-xl p-4 border border-green-200">
                            <div class="flex items-center justify-between">
                                <span class="font-bold text-green-800 text-lg">💵 إجمالي تحصيل اليوم:</span>
                                <span id="total-collection-today" class="font-bold text-green-800 text-2xl">0</span>
                                <span class="font-bold text-green-800">ج.م</span>
                            </div>
                        </div>
                    </div>

                    <div class="space-y-2">
                        <label class="block text-sm font-bold text-gray-700">ملاحظات عامة</label>
                        <textarea id="activity-notes" rows="4" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50 resize-none" placeholder="ملاحظات إضافية عن اليوم..."></textarea>
                    </div>

                    <div class="flex justify-end pt-4 border-t border-gray-100">
                        <button type="submit" id="save-activity-btn" class="bg-gradient-to-r from-teal-500 to-teal-600 text-white px-8 py-3.5 rounded-xl font-bold shadow-lg shadow-teal-500/30 hover:shadow-xl transition-all duration-300 btn-ripple flex items-center gap-2">
                            <i class="ri-save-line text-lg"></i>
                            <span>حفظ النشاط</span>
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </main>
</div>

    <!-- 5. عروض الأسعار -->
    <div id="quote-page" class="min-h-screen flex flex-col hidden page-transition bg-gradient-to-br from-gray-50 to-slate-100">
        <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
            <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
                <div class="flex items-center gap-3">
                    <button type="button" onclick="showPage('user-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الصفحة الرئيسية">
                        <i class="ri-home-4-line text-xl"></i>
                    </button>
                    <h1 class="text-2xl font-bold">Hyma Plastic</h1>
                </div>
                <div class="flex items-center gap-4">
                    <span class="text-sm font-bold" id="quote-page-username"></span>
                    <span class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm" id="quote-page-role"></span>
                    <button type="button" onclick="showPage('profile-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الملف الشخصي">
                        <i class="ri-user-settings-line text-xl"></i>
                    </button>
                </div>
            </div>
        </nav>
        <main class="flex-1 pt-28 pb-16 px-4">
            <div class="max-w-7xl mx-auto">
                <div class="flex flex-wrap justify-between items-center mb-6 gap-4">
                    <h2 class="text-2xl font-bold text-gray-800 flex items-center gap-3">
                        <i class="ri-file-list-line text-green-600 text-3xl"></i>
                        عروض الأسعار
                    </h2>
                    <div class="flex gap-3">
                        <button type="button" id="add-quote-btn" class="bg-gradient-to-r from-green-500 to-green-600 text-white px-5 py-2.5 rounded-xl text-sm font-bold shadow-lg shadow-green-500/30 transition-all flex items-center gap-2 hover:scale-105">
                            <i class="ri-add-line text-lg"></i>
                            <span>إضافة عرض</span>
                        </button>
                    </div>
                </div>
                <div class="table-container overflow-hidden">
                    <div class="overflow-x-auto max-h-[600px] overflow-y-auto">
                        <table class="w-full">
                            <thead class="bg-gray-50 sticky top-0 z-10 shadow-sm">
                                <tr>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">عرض</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">م</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">التاريخ</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">العميل</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">تفاصيل الأصناف</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">طريقة السداد</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">مكان التسليم</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">الحالة</th>
                                    <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">الإجراءات</th>
                                 </tr>
                            </thead>
                            <tbody id="my-quotes-table" class="divide-y divide-gray-100">
                                <tr><td colspan="9" class="px-6 py-12 text-center text-gray-500">لا توجد بيانات</td></tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <!-- صفحة إضافة عرض سعر -->
<div id="add-quote-page" class="min-h-screen flex flex-col hidden page-transition bg-gradient-to-br from-gray-50 to-slate-100">
    <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
        <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <button type="button" onclick="showPage('quote-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الصفحة الرئيسية">
                    <i class="ri-home-4-line text-xl"></i>
                </button>
                <h1 class="text-2xl font-bold">Hyma Plastic</h1>
            </div>
            <div class="flex items-center gap-4">
                <span class="text-sm font-bold" id="add-quote-username"></span>
                <span class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm" id="add-quote-role"></span>
                <button type="button" onclick="showPage('profile-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الملف الشخصي">
                    <i class="ri-user-settings-line text-xl"></i>
                </button>
            </div>
        </div>
    </nav>
    <main class="flex-1 pt-28 pb-16 px-4">
        <div class="max-w-6xl mx-auto">
            <div class="bg-white rounded-2xl shadow-card p-8 border border-gray-100">
                <div class="flex items-center gap-4 mb-8 pb-6 border-b border-gray-100">
                    <div class="w-16 h-16 rounded-2xl bg-gradient-to-br from-green-100 to-green-200 flex items-center justify-center">
                        <i class="ri-file-add-line text-3xl text-green-600"></i>
                    </div>
                    <div>
                        <h2 class="text-2xl font-bold text-gray-800">طلب إصدار عرض سعر</h2>
                        <p class="text-gray-500 text-sm">أدخل تفاصيل عرض السعر</p>
                    </div>
                </div>
                <form id="quote-form" class="space-y-6">
                    <input type="hidden" id="quote-id">
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">التاريخ <span class="text-red-500">*</span></label>
                            <div class="relative">
                                <i class="ri-calendar-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <input type="date" id="quote-date" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50" required>
                            </div>
                        </div>
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">اختر عميلاً</label>
                            <select id="quote-client-select" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50">
                                <option value="">-- اختر عميلاً --</option>
                            </select>
                        </div>
                    </div>

                    <!-- أزرار الضريبة -->
                    <div class="flex justify-start items-center gap-4">
                        <label class="flex items-center gap-2">
                            <input type="radio" name="taxTypeQuote" value="exclusive" class="tax-radio-quote custom-checkbox" checked> غير شامل الضريبة
                        </label>
                        <label class="flex items-center gap-2">
                            <input type="radio" name="taxTypeQuote" value="inclusive" class="tax-radio-quote custom-checkbox"> شامل الضريبة
                        </label>
                    </div>

                    <!-- جدول الأصناف مع سعر الوحدة والإجمالي (بدون خصم) -->
                    <div class="space-y-3">
                        <label class="block text-sm font-bold text-gray-700">تفاصيل الأصناف</label>
                        <div class="overflow-x-auto rounded-xl border border-gray-200">
                            <table class="dynamic-table" id="quote-items-table" style="table-layout: fixed;">
                                <thead>
                                    <tr class="bg-gray-50">
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700" style="width: 5%">#</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700" style="width: 15%">كود الصنف</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700" style="width: 20%">اسم الصنف</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700" style="width: 8%">الكمية</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700" style="width: 10%">الوحدة</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700" style="width: 12%">سعر الوحدة</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700" style="width: 12%">الإجمالي</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700" style="width: 8%">الإجراءات</th>
                                    </tr>
                                </thead>
                                <tbody id="quote-items-body">
                                    <!-- سيتم إضافة صف واحد -->
                                </tbody>
                            </table>
                        </div>
                        <!-- ملخص الضرائب والإجماليات -->
                        <div class="mt-4 flex flex-col items-end gap-3">
                            <div class="bg-gradient-to-r from-gray-50 to-gray-100 px-6 py-3 rounded-xl border">
                                <span class="font-bold text-gray-700">الإجمالي قبل الضريبة: </span>
                                <span id="quote-subtotal-before-tax" class="font-bold text-primary text-xl">0</span>
                                <span class="font-bold text-gray-700"> ج.م</span>
                            </div>
                            <div class="bg-gradient-to-r from-gray-50 to-gray-100 px-6 py-3 rounded-xl border">
                                <span class="font-bold text-gray-700">إجمالي الضريبة (14%): </span>
                                <span id="quote-total-tax" class="font-bold text-primary text-xl">0</span>
                                <span class="font-bold text-gray-700"> ج.م</span>
                            </div>
                            <div class="bg-gradient-to-r from-gray-50 to-gray-100 px-6 py-3 rounded-xl border">
                                <span class="font-bold text-gray-700">الإجمالي الكلي (شامل الضريبة): </span>
                                <span id="quote-total-amount" class="font-bold text-primary text-xl">0</span>
                                <span class="font-bold text-gray-700"> ج.م</span>
                            </div>
                        </div>
                    </div>

                    <!-- طريقة السداد + مدة العرض -->
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">طريقة السداد</label>
                            <input type="text" id="quote-payment-method" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl" placeholder="مثلاً: نقدي / أجل">
                        </div>
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">مدة العرض</label>
                            <select id="quote-validity" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl">
                                <option value="30 يوم">30 يوم</option>
                                <option value="اسبوعين">اسبوعين</option>
                                <option value="اسبوع">اسبوع</option>
                                <option value="10 ايام">10 ايام</option>
                                <option value="2 يوم">2 يوم</option>
                                <option value="1 يوم">1 يوم</option>
                            </select>
                        </div>
                    </div>

                    <div class="space-y-2">
                        <label class="block text-sm font-bold text-gray-700">مكان التسليم</label>
                        <select id="quote-delivery-place" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl">
                            <option value="">اختر مكان التسليم</option>
                            <option value="استلام المصنع">استلام المصنع</option>
                            <option value="مخازن العميل">مخازن العميل</option>
                        </select>
                    </div>

                    <div class="space-y-2">
                        <label class="block text-sm font-bold text-gray-700">ملاحظات</label>
                        <textarea id="quote-notes" rows="4" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl resize-none"></textarea>
                    </div>

                    <div class="flex justify-end pt-4 border-t border-gray-100">
                        <button type="submit" id="save-quote-btn" class="bg-gradient-to-r from-green-500 to-green-600 text-white px-8 py-3.5 rounded-xl font-bold shadow-lg shadow-green-500/30 hover:shadow-xl transition-all duration-300 btn-ripple flex items-center gap-2">
                            <i class="ri-save-line text-lg"></i>
                            <span>حفظ عرض السعر</span>
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </main>
</div>

    <!-- 6. أوامر البيع -->
    <!-- ===== صفحة أوامر البيع (قائمة) ===== -->
<div id="sales-page" class="min-h-screen flex flex-col hidden page-transition bg-gradient-to-br from-gray-50 to-slate-100">
    <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
        <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <button type="button" onclick="showPage('user-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الصفحة الرئيسية">
                    <i class="ri-home-4-line text-xl"></i>
                </button>
                <h1 class="text-2xl font-bold">Hyma Plastic</h1>
            </div>
            <div class="flex items-center gap-4">
                <span class="text-sm font-bold" id="sale-page-username"></span>
                <span class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm" id="sale-page-role"></span>
                <button type="button" onclick="showPage('profile-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الملف الشخصي">
                    <i class="ri-user-settings-line text-xl"></i>
                </button>
            </div>
        </div>
    </nav>
    <main class="flex-1 pt-28 pb-16 px-4">
        <div class="max-w-7xl mx-auto">
            <div class="flex flex-wrap justify-between items-center mb-6 gap-4">
                <h2 class="text-2xl font-bold text-gray-800 flex items-center gap-3">
                    <i class="ri-line-chart-line text-blue-600 text-3xl"></i>
                    أوامر البيع
                </h2>
                <div class="flex gap-3">
                    <button type="button" id="add-sale-btn" class="bg-gradient-to-r from-blue-500 to-blue-600 text-white px-5 py-2.5 rounded-xl text-sm font-bold shadow-lg shadow-blue-500/30 transition-all flex items-center gap-2 hover:scale-105">
                        <i class="ri-add-line text-lg"></i>
                        <span>إضافة أمر</span>
                    </button>
                </div>
            </div>
            <div class="table-container overflow-hidden">
                <div class="overflow-x-auto max-h-[600px] overflow-y-auto">
                    <table class="w-full">
                        <thead class="bg-gray-50 sticky top-0 z-10 shadow-sm">
                            <tr>
                                <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">عرض</th>
                                <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">م</th>
                                <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">التاريخ</th>
                                <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">العميل</th>
                                <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">تفاصيل الأصناف</th>
                                <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">مكان التصنيع</th>
                                <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">طريقة السداد</th>
                                <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">مكان التسليم</th>
                                <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">الحالة</th>
                                <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">ملاحظات</th>
                                <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">الإجراءات</th>
                             </tr>
                        </thead>
                        <tbody id="my-sales-table" class="divide-y divide-gray-100">
                            <tr><td colspan="11" class="px-6 py-12 text-center text-gray-500">لا توجد بيانات</td></tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </main>
</div>

<!-- ===== صفحة إضافة أمر بيع (معدلة بالحقول الجديدة) ===== -->
<div id="add-sales-page" class="min-h-screen flex flex-col hidden page-transition bg-gradient-to-br from-gray-50 to-slate-100">
    <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
        <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <button type="button" onclick="showPage('sales-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الصفحة الرئيسية">
                    <i class="ri-home-4-line text-xl"></i>
                </button>
                <h1 class="text-2xl font-bold">Hyma Plastic</h1>
            </div>
            <div class="flex items-center gap-4">
                <span class="text-sm font-bold" id="add-sale-username"></span>
                <span class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm" id="add-sale-role"></span>
                <button type="button" onclick="showPage('profile-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الملف الشخصي">
                    <i class="ri-user-settings-line text-xl"></i>
                </button>
            </div>
        </div>
    </nav>
    <main class="flex-1 pt-28 pb-16 px-4">
        <div class="max-w-6xl mx-auto">
            <div class="bg-white rounded-2xl shadow-card p-8 border border-gray-100">
                <div class="flex items-center gap-4 mb-8 pb-6 border-b border-gray-100">
                    <div class="w-16 h-16 rounded-2xl bg-gradient-to-br from-blue-100 to-blue-200 flex items-center justify-center">
                        <i class="ri-shopping-cart-add-line text-3xl text-blue-600"></i>
                    </div>
                    <div>
                        <h2 class="text-2xl font-bold text-gray-800">أمر بيع</h2>
                        <p class="text-gray-500 text-sm">أدخل تفاصيل أمر البيع</p>
                    </div>
                </div>
                <form id="sale-form" class="space-y-6">
                    <input type="hidden" id="sale-id">
                    
                    <!-- الصف الأول: التاريخ واسم العميل -->
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">التاريخ <span class="text-red-500">*</span></label>
                            <div class="relative">
                                <i class="ri-calendar-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <input type="date" id="sale-date" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50" required>
                            </div>
                        </div>
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">اختر عميلاً</label>
                            <select id="sale-client-select" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50">
                                <option value="">-- اختر عميلاً --</option>
                            </select>
                        </div>
                    </div>

                    <!-- أزرار الضريبة وزر مبني على -->
                    <div class="flex justify-between items-center gap-4">
                        <div class="flex gap-4">
                            <label class="flex items-center gap-2">
                                <input type="radio" name="taxType" value="exclusive" class="tax-radio custom-checkbox" checked> غير شامل الضريبة
                            </label>
                            <label class="flex items-center gap-2">
                                <input type="radio" name="taxType" value="inclusive" class="tax-radio custom-checkbox"> شامل الضريبة
                            </label>
                        </div>
                        <button type="button" id="based-on-btn" class="bg-gradient-to-r from-amber-500 to-amber-600 text-white px-6 py-2.5 rounded-xl text-sm font-bold shadow-lg shadow-amber-500/30 transition-all flex items-center gap-2 hover:scale-105">
                            <i class="ri-stackshare-line text-lg"></i>
                            <span>مبني على</span>
                        </button>
                    </div>

                    <!-- جدول الأصناف مع إضافة عمود نسبة الخصم -->
                    <div class="space-y-3">
                        <label class="block text-sm font-bold text-gray-700">تفاصيل الأصناف</label>
                        <div class="overflow-x-auto rounded-xl border border-gray-200">
                            <table class="dynamic-table" id="sale-items-table" style="table-layout: fixed;">
                                <thead>
                                    <tr class="bg-gray-50">
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700" style="width: 5%">#</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700" style="width: 15%">كود الصنف</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700" style="width: 20%">اسم الصنف</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700" style="width: 8%">الكمية</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700" style="width: 10%">الوحدة</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700" style="width: 12%">سعر الوحدة</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700" style="width: 8%">نسبة الخصم %</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700" style="width: 12%">الإجمالي بعد الخصم</th>
                                        <th class="px-4 py-3 text-sm font-bold text-gray-700" style="width: 8%">الإجراءات</th>
                                     </tr>
                                </thead>
                                <tbody id="sale-items-body">
                                    <!-- سيتم إضافة صف واحد فقط -->
                                </tbody>
                             </table>
                        </div>
                        
                        <!-- ملخص الضرائب والإجماليات -->
                        <div class="mt-4 flex flex-col items-end gap-3">
                            <div class="bg-gradient-to-r from-gray-50 to-gray-100 px-6 py-3 rounded-xl border">
                                <span class="font-bold text-gray-700">الإجمالي قبل الضريبة: </span>
                                <span id="subtotal-before-tax" class="font-bold text-primary text-xl">0</span>
                                <span class="font-bold text-gray-700"> ج.م</span>
                            </div>
                            <div class="bg-gradient-to-r from-gray-50 to-gray-100 px-6 py-3 rounded-xl border">
                                <span class="font-bold text-gray-700">إجمالي الضريبة (14%): </span>
                                <span id="sale-total-tax" class="font-bold text-primary text-xl">0</span>
                                <span class="font-bold text-gray-700"> ج.م</span>
                            </div>
                            <div class="bg-gradient-to-r from-gray-50 to-gray-100 px-6 py-3 rounded-xl border">
                                <span class="font-bold text-gray-700">الإجمالي الكلي (شامل الضريبة): </span>
                                <span id="sale-total-amount" class="font-bold text-primary text-xl">0</span>
                                <span class="font-bold text-gray-700"> ج.م</span>
                            </div>
                        </div>
                    </div>

                    <!-- مكان التصنيع، طريقة السداد، مكان التسليم -->
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">مكان التصنيع</label>
                            <select id="sale-manufacturing-location" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50">
                                <option value="">اختر مكان التصنيع</option>
                                <option value="مصنع المنصورية">مصنع المنصورية</option>
                                <option value="مصنع ابو رواش">مصنع ابو رواش</option>
                                <option value="مصنع العين السخنة">مصنع العين السخنة</option>
                            </select>
                        </div>
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">طريقة السداد</label>
                            <input type="text" id="sale-payment-method" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl" placeholder="مثلاً: نقدي / أجل">
                        </div>
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">مكان التسليم</label>
                            <select id="sale-delivery-place" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl">
                                <option value="">اختر مكان التسليم</option>
                                <option value="استلام المصنع">استلام المصنع</option>
                                <option value="مخازن العميل">مخازن العميل</option>
                            </select>
                        </div>
                    </div>

                    <!-- الشروط والأحكام -->
                    <div class="space-y-2">
                        <label class="block text-sm font-bold text-gray-700">الشروط والأحكام</label>
                        <textarea id="terms-conditions" rows="4" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl resize-none" placeholder="مثال: السداد خلال أسبوع من الاستلام، العملة بالجنيه المصري..."></textarea>
                    </div>

                    <!-- ملاحظات إضافية -->
                    <div class="space-y-2">
                        <label class="block text-sm font-bold text-gray-700">ملاحظات</label>
                        <textarea id="sale-notes" rows="3" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl resize-none"></textarea>
                    </div>

                    <div class="flex justify-end pt-4 border-t border-gray-100">
                        <button type="submit" id="save-sale-btn" class="bg-gradient-to-r from-blue-500 to-blue-600 text-white px-8 py-3.5 rounded-xl font-bold shadow-lg shadow-blue-500/30 hover:shadow-xl transition-all duration-300 btn-ripple flex items-center gap-2">
                            <i class="ri-save-line text-lg"></i>
                            <span>حفظ أمر البيع</span>
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </main>
</div>

    <!-- 7. شكاوى العملاء -->
    <div id="complaints-page" class="min-h-screen flex flex-col hidden page-transition bg-gradient-to-br from-gray-50 to-slate-100">
    <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
        <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <button type="button" onclick="showPage('user-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الصفحة الرئيسية">
                    <i class="ri-home-4-line text-xl"></i>
                </button>
                <h1 class="text-2xl font-bold">Hyma Plastic</h1>
            </div>
            <div class="flex items-center gap-4">
                <span class="text-sm font-bold" id="complaint-page-username"></span>
                <span class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm" id="complaint-page-role"></span>
                <button type="button" onclick="showPage('profile-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الملف الشخصي">
                    <i class="ri-user-settings-line text-xl"></i>
                </button>
            </div>
        </div>
    </nav>
    <main class="flex-1 pt-28 pb-16 px-4">
        <div class="max-w-7xl mx-auto">
            <div class="flex flex-wrap justify-between items-center mb-6 gap-4">
                <h2 class="text-2xl font-bold text-gray-800 flex items-center gap-3">
                    <i class="ri-alert-line text-orange-600 text-3xl"></i>
                    شكاوى العملاء
                </h2>
                <div class="flex gap-3">
                    <button type="button" id="add-complaint-btn" class="bg-gradient-to-r from-orange-500 to-orange-600 text-white px-5 py-2.5 rounded-xl text-sm font-bold shadow-lg shadow-orange-500/30 transition-all flex items-center gap-2 hover:scale-105">
                        <i class="ri-add-line text-lg"></i>
                        <span>إضافة شكوى</span>
                    </button>
                </div>
            </div>
            <div class="table-container overflow-hidden">
                <div class="overflow-x-auto max-h-[600px] overflow-y-auto">
                    <table class="w-full">
                        <thead class="bg-gray-50 sticky top-0 z-10 shadow-sm">
                            <tr>
                                <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">عرض</th>
                                <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">م</th>
                                <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">التاريخ</th>
                                <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">العميل</th>
                                <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">الكمية</th>
                                <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">الوحدة</th>
                                <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">رقم الهاتف</th>
                                <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">مسؤول التواصل</th>
                                <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">رقم مسؤول التواصل</th>
                                <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">طريقة الشكوى</th>
                                <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">النوع</th>
                                <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">الحالة</th>
                                <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">الوصف</th>
                                <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">المرفق</th>
                                <th class="px-4 py-4 text-center text-sm font-bold text-gray-700 border-b">الإجراءات</th>
                              </tr>
                        </thead>
                        <tbody id="my-complaints-table" class="divide-y divide-gray-100">
                            <tr><td colspan="15" class="px-6 py-12 text-center text-gray-500">لا توجد بيانات</td></tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </main>
</div>

<!-- صفحة إضافة شكوى -->
<div id="add-complaint-page" class="min-h-screen flex flex-col hidden page-transition bg-gradient-to-br from-gray-50 to-slate-100">
    <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
        <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <button type="button" onclick="showPage('complaints-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الصفحة الرئيسية">
                    <i class="ri-home-4-line text-xl"></i>
                </button>
                <h1 class="text-2xl font-bold">Hyma Plastic</h1>
            </div>
            <div class="flex items-center gap-4">
                <span class="text-sm font-bold" id="add-complaint-username"></span>
                <span class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm" id="add-complaint-role"></span>
                <button type="button" onclick="showPage('profile-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الملف الشخصي">
                    <i class="ri-user-settings-line text-xl"></i>
                </button>
            </div>
        </div>
    </nav>
    <main class="flex-1 pt-28 pb-16 px-4">
        <div class="max-w-4xl mx-auto">
            <div class="bg-white rounded-2xl shadow-card p-8 border border-gray-100">
                <div class="flex items-center gap-4 mb-8 pb-6 border-b border-gray-100">
                    <div class="w-16 h-16 rounded-2xl bg-gradient-to-br from-orange-100 to-orange-200 flex items-center justify-center">
                        <i class="ri-alert-add-line text-3xl text-orange-600"></i>
                    </div>
                    <div>
                        <h2 class="text-2xl font-bold text-gray-800">شكاوى العملاء</h2>
                        <p class="text-gray-500 text-sm">سجل شكوى العميل بشكل مفصل</p>
                    </div>
                </div>
                <form id="complaint-form" class="space-y-6">
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">التاريخ <span class="text-red-500">*</span></label>
                            <div class="relative">
                                <i class="ri-calendar-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <input type="date" id="complaint-date" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50" required>
                            </div>
                        </div>
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">اختر عميلاً</label>
                            <select id="complaint-client-select" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50">
                                <option value="">-- اختر عميلاً --</option>
                            </select>
                        </div>
                    </div>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">رقم الهاتف</label>
                            <div class="relative">
                                <i class="ri-phone-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <input type="tel" id="complaint-phone" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50">
                            </div>
                        </div>
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">البريد الإلكتروني</label>
                            <div class="relative">
                                <i class="ri-mail-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <input type="email" id="complaint-email" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50">
                            </div>
                        </div>
                    </div>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">مسؤول التواصل</label>
                            <div class="relative">
                                <i class="ri-user-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <input type="text" id="complaint-contact-person" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50">
                            </div>
                        </div>
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">رقم مسؤول التواصل</label>
                            <div class="relative">
                                <i class="ri-phone-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <input type="tel" id="complaint-contact-phone" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50">
                            </div>
                        </div>
                    </div>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">الكمية</label>
                            <div class="relative">
                                <i class="ri-hashtag absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <input type="number" id="complaint-qty" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50">
                            </div>
                        </div>
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">الوحدة</label>
                            <div class="relative">
                                <i class="ri-scales-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <select id="complaint-unit" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50 appearance-none">
                                    <option value="">اختر الوحدة</option>
                                    <option value="كيلو">كيلو</option>
                                    <option value="طن">طن</option>
                                    <option value="متر">متر</option>
                                    <option value="متر مربع">متر مربع</option>
                                    <option value="عدد">عدد</option>
                                </select>
                                <i class="ri-arrow-down-s-line absolute left-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg pointer-events-none"></i>
                            </div>
                        </div>
                    </div>
                    <div class="space-y-2">
                        <label class="block text-sm font-bold text-gray-700">نوع الشكوى</label>
                        <div class="relative">
                            <i class="ri-flag-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                            <select id="complaint-type" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50 appearance-none">
                                <option value="">اختر النوع</option>
                                <option value="منتج">منتج</option>
                                <option value="خدمة">خدمة</option>
                                <option value="توصيل">توصيل</option>
                                <option value="أخرى">أخرى</option>
                            </select>
                            <i class="ri-arrow-down-s-line absolute left-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg pointer-events-none"></i>
                        </div>
                    </div>
                    <div class="space-y-2">
                        <label class="block text-sm font-bold text-gray-700">طريقة عمل الشكوى</label>
                        <div class="relative">
                            <i class="ri-chat-1-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                            <select id="complaint-method" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50 appearance-none">
                                <option value="">اختر الطريقة</option>
                                <option value="تليفونياً">تليفونياً</option>
                                <option value="بريد إلكتروني">بريد إلكتروني</option>
                                <option value="واتساب">واتساب</option>
                                <option value="مكان العميل">مكان العميل</option>
                            </select>
                            <i class="ri-arrow-down-s-line absolute left-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg pointer-events-none"></i>
                        </div>
                    </div>
                    <div class="space-y-2">
                        <label class="block text-sm font-bold text-gray-700">الوصف</label>
                        <textarea id="complaint-description" rows="5" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50 resize-none" placeholder="اكتب وصف تفصيلي للشكوى..."></textarea>
                    </div>
                    <div class="space-y-2">
                        <label class="block text-sm font-bold text-gray-700">المرفقات (صور، مستندات)</label>
                        <div class="relative">
                            <input type="file" id="complaint-attachments" multiple class="file-input-primary w-full px-4 py-3 border-2 border-dashed border-gray-300 rounded-xl hover:border-primary transition-colors bg-gray-50/50" accept=".jpg,.jpeg,.png,.pdf,.doc,.docx">
                        </div>
                        <p class="text-xs text-gray-500 mt-1">يمكنك رفع عدة ملفات كدليل على الشكوى</p>
                    </div>
                    <div class="flex justify-end pt-4 border-t border-gray-100">
                        <button type="submit" id="save-complaint-btn" class="bg-gradient-to-r from-orange-500 to-orange-600 text-white px-8 py-3.5 rounded-xl font-bold shadow-lg shadow-orange-500/30 hover:shadow-xl transition-all duration-300 btn-ripple flex items-center gap-2">
                            <i class="ri-save-line text-lg"></i>
                            <span>حفظ الشكوى</span>
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </main>
</div>

<!-- 8. متابعة التحصيلات -->
<div id="collections-page" class="min-h-screen flex flex-col hidden page-transition bg-gradient-to-br from-gray-50 to-slate-100">
    <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
        <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <button type="button" onclick="showPage('user-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الصفحة الرئيسية">
                    <i class="ri-home-4-line text-xl"></i>
                </button>
                <h1 class="text-2xl font-bold">Hyma Plastic</h1>
            </div>
            <div class="flex items-center gap-4">
                <span class="text-sm font-bold" id="collection-page-username"></span>
                <span class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm" id="collection-page-role"></span>
                <button type="button" onclick="showPage('profile-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الملف الشخصي">
                    <i class="ri-user-settings-line text-xl"></i>
                </button>
            </div>
        </div>
    </nav>
    <main class="flex-1 pt-28 pb-16 px-4">
        <div class="max-w-7xl mx-auto">
            <div class="flex flex-wrap justify-between items-center mb-6 gap-4">
                <h2 class="text-2xl font-bold text-gray-800 flex items-center gap-3">
                    <i class="ri-money-dollar-circle-line text-amber-600 text-3xl"></i>
                    متابعة التحصيلات
                </h2>
                <div class="flex gap-3">
                    <button type="button" id="add-collection-btn" class="bg-gradient-to-r from-amber-500 to-amber-600 text-white px-5 py-2.5 rounded-xl text-sm font-bold shadow-lg shadow-amber-500/30 transition-all flex items-center gap-2 hover:scale-105">
                        <i class="ri-add-line text-lg"></i>
                        <span>إضافة تحصيل</span>
                    </button>
                </div>
            </div>
            <div class="table-container overflow-hidden">
                <div class="overflow-x-auto max-h-[600px] overflow-y-auto">
                    <table class="w-full">
                        <thead class="bg-gray-50 sticky top-0 z-10 shadow-sm">
                            <tr>
                                <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">عرض</th>
                                <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">م</th>
                                <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">التاريخ</th>
                                <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">العميل</th>
                                <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">المبلغ المستحق</th>
                                <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">تاريخ الاستحقاق</th>
                                <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">الحالة</th>
                                <th class="px-6 py-4 text-center text-sm font-bold text-gray-700 border-b">ملاحظات</th>
                              </tr>
                        </thead>
                        <tbody id="my-collections-table" class="divide-y divide-gray-100">
                            <tr><td colspan="8" class="px-6 py-12 text-center text-gray-500">لا توجد بيانات</td></tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </main>
</div>

<!-- صفحة إضافة تحصيل -->
<div id="add-collection-page" class="min-h-screen flex flex-col hidden page-transition bg-gradient-to-br from-gray-50 to-slate-100">
    <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
        <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <button type="button" onclick="showPage('collections-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الصفحة الرئيسية">
                    <i class="ri-home-4-line text-xl"></i>
                </button>
                <h1 class="text-2xl font-bold">Hyma Plastic</h1>
            </div>
            <div class="flex items-center gap-4">
                <span class="text-sm font-bold" id="add-collection-username"></span>
                <span class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm" id="add-collection-role"></span>
                <button type="button" onclick="showPage('profile-page')" class="hover:bg-white/20 p-2.5 rounded-xl transition-all nav-item" title="الملف الشخصي">
                    <i class="ri-user-settings-line text-xl"></i>
                </button>
            </div>
        </div>
    </nav>
    <main class="flex-1 pt-28 pb-16 px-4">
        <div class="max-w-4xl mx-auto">
            <div class="bg-white rounded-2xl shadow-card p-8 border border-gray-100">
                <div class="flex items-center gap-4 mb-8 pb-6 border-b border-gray-100">
                    <div class="w-16 h-16 rounded-2xl bg-gradient-to-br from-amber-100 to-amber-200 flex items-center justify-center">
                        <i class="ri-money-cny-circle-line text-3xl text-amber-600"></i>
                    </div>
                    <div>
                        <h2 class="text-2xl font-bold text-gray-800">متابعة التحصيلات</h2>
                        <p class="text-gray-500 text-sm">سجل بيانات التحصيل من العميل</p>
                    </div>
                </div>
                <form id="collection-form" class="space-y-6">
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">التاريخ <span class="text-red-500">*</span></label>
                            <div class="relative">
                                <i class="ri-calendar-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <input type="date" id="collection-date" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50" required>
                            </div>
                        </div>
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">اختر عميلاً</label>
                            <select id="collection-client-select" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50">
                                <option value="">-- اختر عميلاً --</option>
                            </select>
                        </div>
                    </div>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">المبلغ المستحق <span class="text-red-500">*</span></label>
                            <div class="relative">
                                <i class="ri-money-dollar-circle-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <input type="number" id="collection-amount" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50" required>
                            </div>
                        </div>
                        <div class="space-y-2">
                            <label class="block text-sm font-bold text-gray-700">تاريخ الاستحقاق</label>
                            <div class="relative">
                                <i class="ri-calendar-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                                <input type="date" id="collection-due" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50">
                            </div>
                        </div>
                    </div>
                    <div class="space-y-2">
                        <label class="block text-sm font-bold text-gray-700">الحالة <span class="text-red-500">*</span></label>
                        <div class="relative">
                            <i class="ri-flag-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg"></i>
                            <select id="collection-status" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50 appearance-none" required>
                                <option value="">اختر الحالة</option>
                                <option value="مدفوع">مدفوع</option>
                                <option value="غير مدفوع">غير مدفوع</option>
                                <option value="جزئي">جزئي</option>
                                <option value="متأخر">متأخر</option>
                            </select>
                            <i class="ri-arrow-down-s-line absolute left-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg pointer-events-none"></i>
                        </div>
                    </div>
                    <div class="space-y-2">
                        <label class="block text-sm font-bold text-gray-700">ملاحظات</label>
                        <textarea id="collection-notes" rows="4" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50 resize-none"></textarea>
                    </div>
                    <div class="flex justify-end pt-4 border-t border-gray-100">
                        <button type="submit" id="save-collection-btn" class="bg-gradient-to-r from-amber-500 to-amber-600 text-white px-8 py-3.5 rounded-xl font-bold shadow-lg shadow-amber-500/30 hover:shadow-xl transition-all duration-300 btn-ripple flex items-center gap-2">
                            <i class="ri-save-line text-lg"></i>
                            <span>حفظ التحصيل</span>
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </main>
</div>



<!-- ===== المودالات ===== -->
<div id="quotes-list-modal" class="fixed inset-0 flex items-center justify-center z-50 modal-backdrop hidden">
    <div class="bg-white rounded-2xl p-6 w-full max-w-4xl mx-4 max-h-[85vh] overflow-y-auto shadow-2xl border border-gray-100 animate-slide-up">
        <div class="flex justify-between items-center mb-6 pb-4 border-b border-gray-100">
            <h3 class="text-xl font-bold text-gray-800 flex items-center gap-2">
                <i class="ri-stackshare-line text-amber-500"></i>
                عروض الأسعار المعتمدة
            </h3>
            <button onclick="document.getElementById('quotes-list-modal').classList.add('hidden')" class="text-gray-400 hover:text-gray-600 transition-colors p-2 hover:bg-gray-100 rounded-lg">
                <i class="ri-close-line text-2xl"></i>
            </button>
        </div>
        <div class="mb-4 flex gap-4">
            <div class="flex-1 relative">
                <i class="ri-search-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400"></i>
                <input type="text" id="quote-search-input" class="w-full pr-12 pl-4 py-3 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all" placeholder="بحث برقم المستند أو اسم العميل...">
            </div>
            <button onclick="basedOnSelectedQuotes()" class="bg-gradient-to-r from-amber-500 to-amber-600 text-white px-6 py-3 rounded-xl font-bold shadow-lg shadow-amber-500/30 hover:shadow-xl transition-all flex items-center gap-2">
                <i class="ri-check-line"></i>
                <span>مبني على المحدد</span>
            </button>
        </div>
        <div class="overflow-x-auto">
            <table class="w-full">
                <thead class="bg-gray-50 sticky top-0 z-10">
                    <tr>
                        <th class="px-4 py-3 text-center text-sm font-bold text-gray-700 border-b"><input type="checkbox" id="select-all-quotes-modal" onclick="toggleAllQuotesModal()" class="custom-checkbox"></th>
                        <th class="px-4 py-3 text-center text-sm font-bold text-gray-700 border-b">رقم المستند</th>
                        <th class="px-4 py-3 text-center text-sm font-bold text-gray-700 border-b">التاريخ</th>
                        <th class="px-4 py-3 text-center text-sm font-bold text-gray-700 border-b">العميل</th>
                        <th class="px-4 py-3 text-center text-sm font-bold text-gray-700 border-b">تفاصيل الأصناف</th>
                     </tr>
                </thead>
                <tbody id="approved-quotes-list" class="divide-y divide-gray-100">
                    <!-- سيتم ملؤه بالبيانات -->
                </tbody>
            </table>
        </div>
    </div>
</div>

<!-- مودال سبب الرفض -->
<div id="rejection-reason-modal" class="fixed inset-0 flex items-center justify-center z-50 modal-backdrop hidden">
    <div class="bg-white rounded-2xl p-6 w-full max-w-md mx-4 shadow-2xl border border-gray-100 animate-slide-up">
        <div class="flex justify-between items-center mb-6 pb-4 border-b border-gray-100">
            <h3 class="text-xl font-bold text-gray-800 flex items-center gap-2">
                <i class="ri-close-circle-line text-red-500"></i>
                سبب الرفض
            </h3>
            <button onclick="closeRejectionModal()" class="text-gray-400 hover:text-gray-600 transition-colors p-2 hover:bg-gray-100 rounded-lg">
                <i class="ri-close-line text-2xl"></i>
            </button>
        </div>
        <div class="space-y-4">
            <input type="hidden" id="rejection-type">
            <input type="hidden" id="rejection-ids">
            <div class="space-y-2">
                <label class="block text-sm font-bold text-gray-700">سبب الرفض <span class="text-red-500">*</span></label>
                <textarea id="rejection-reason-text" rows="4" class="w-full px-4 py-3 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all resize-none" placeholder="اكتب سبب الرفض هنا..."></textarea>
            </div>
            <div class="flex gap-3 pt-4">
                <button onclick="confirmRejection()" class="flex-1 bg-gradient-to-r from-red-500 to-red-600 text-white py-3 rounded-xl font-bold shadow-lg shadow-red-500/30 hover:shadow-xl transition-all flex items-center justify-center gap-2">
                    <i class="ri-check-line"></i>
                    <span>تأكيد الرفض</span>
                </button>
                <button onclick="closeRejectionModal()" class="flex-1 bg-gray-100 hover:bg-gray-200 text-gray-700 py-3 rounded-xl font-bold transition-all flex items-center justify-center gap-2">
                    <i class="ri-close-line"></i>
                    <span>إلغاء</span>
                </button>
            </div>
        </div>
    </div>
</div>

<!-- مودال عرض سبب الرفض -->
<div id="view-rejection-modal" class="fixed inset-0 flex items-center justify-center z-50 modal-backdrop hidden">
    <div class="bg-white rounded-2xl p-6 w-full max-w-md mx-4 shadow-2xl border border-gray-100 animate-slide-up">
        <div class="flex justify-between items-center mb-6 pb-4 border-b border-gray-100">
            <h3 class="text-xl font-bold text-gray-800 flex items-center gap-2">
                <i class="ri-information-line text-orange-500"></i>
                سبب الرفض
            </h3>
            <button onclick="document.getElementById('view-rejection-modal').classList.add('hidden')" class="text-gray-400 hover:text-gray-600 transition-colors p-2 hover:bg-gray-100 rounded-lg">
                <i class="ri-close-line text-2xl"></i>
            </button>
        </div>
        <div class="bg-red-50 border-2 border-red-200 rounded-xl p-4 mb-4">
            <p id="view-rejection-text" class="text-red-800 font-medium leading-relaxed"></p>
        </div>
        <div class="text-center">
            <button onclick="document.getElementById('view-rejection-modal').classList.add('hidden')" class="bg-gray-100 hover:bg-gray-200 text-gray-700 px-8 py-3 rounded-xl font-bold transition-all">
                إغلاق
            </button>
        </div>
    </div>
</div>

<!-- مودال إرسال البريد الإلكتروني -->
<div id="email-send-modal" class="fixed inset-0 flex items-center justify-center z-50 modal-backdrop hidden">
    <div class="bg-white rounded-2xl p-6 w-full max-w-lg mx-4 shadow-2xl border border-gray-100 animate-slide-up">
        <div class="flex justify-between items-center mb-6 pb-4 border-b border-gray-100">
            <h3 class="text-xl font-bold text-gray-800 flex items-center gap-2">
                <i class="ri-mail-send-line text-primary"></i>
                إرسال البريد الإلكتروني
            </h3>
            <button onclick="closeEmailModal()" class="text-gray-400 hover:text-gray-600 transition-colors p-2 hover:bg-gray-100 rounded-lg">
                <i class="ri-close-line text-2xl"></i>
            </button>
        </div>
        <form id="email-send-form" class="space-y-4">
            <input type="hidden" id="email-doc-type">
            <input type="hidden" id="email-doc-ids">
            
            <div class="space-y-2">
                <label class="block text-sm font-bold text-gray-700">عنوان البريد الإلكتروني <span class="text-red-500">*</span></label>
                <div class="relative">
                    <i class="ri-mail-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400"></i>
                    <input type="email" id="email-recipient" class="w-full pr-12 pl-4 py-3 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all" placeholder="example@domain.com" required>
                </div>
            </div>
            
            <div class="space-y-2">
                <label class="block text-sm font-bold text-gray-700">عنوان الرسالة</label>
                <div class="relative">
                    <i class="ri-heading absolute right-4 top-1/2 -translate-y-1/2 text-gray-400"></i>
                    <input type="text" id="email-subject" class="w-full pr-12 pl-4 py-3 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all" placeholder="عنوان الرسالة">
                </div>
            </div>
            
            <div class="space-y-2">
                <label class="block text-sm font-bold text-gray-700">نص الرسالة</label>
                <textarea id="email-body" rows="4" class="w-full px-4 py-3 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all resize-none" placeholder="نص الرسالة الإضافي..."></textarea>
            </div>
            
            <div class="bg-blue-50 border border-blue-200 rounded-xl p-3">
                <p class="text-sm text-blue-800 flex items-center gap-2">
                    <i class="ri-information-line"></i>
                    سيتم إرفاق المستندات المحددة كملفات PDF مع الرسالة
                </p>
            </div>
            
            <div class="flex gap-3 pt-4">
                <button type="submit" class="flex-1 bg-gradient-to-r from-primary to-primaryDark text-white py-3 rounded-xl font-bold shadow-lg shadow-primary/30 hover:shadow-xl transition-all flex items-center justify-center gap-2">
                    <i class="ri-send-plane-line"></i>
                    <span>إرسال</span>
                </button>
                <button type="button" onclick="closeEmailModal()" class="flex-1 bg-gray-100 hover:bg-gray-200 text-gray-700 py-3 rounded-xl font-bold transition-all flex items-center justify-center gap-2">
                    <i class="ri-close-line"></i>
                    <span>إلغاء</span>
                </button>
            </div>
        </form>
    </div>
</div>

<!-- تعديل المستخدم -->
<div id="edit-user-modal" class="fixed inset-0 flex items-center justify-center z-50 modal-backdrop hidden">
    <div class="bg-white rounded-2xl p-8 w-full max-w-md mx-4 shadow-2xl border border-gray-100 animate-slide-up">
        <div class="flex justify-between items-center mb-6 pb-4 border-b border-gray-100">
            <h3 class="text-xl font-bold text-gray-800 flex items-center gap-2">
                <i class="ri-user-edit-line text-primary"></i>
                تعديل بيانات المستخدم
            </h3>
            <button onclick="document.getElementById('edit-user-modal').classList.add('hidden')" class="text-gray-400 hover:text-gray-600 transition-colors p-2 hover:bg-gray-100 rounded-lg">
                <i class="ri-close-line text-2xl"></i>
            </button>
        </div>
        <form id="edit-user-form" class="space-y-5">
            <input type="hidden" id="edit-original-username">
            <div class="space-y-2">
                <label class="block text-sm font-bold text-gray-700">اسم المستخدم</label>
                <div class="relative">
                    <i class="ri-user-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400"></i>
                    <input type="text" id="edit-username" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus" required>
                </div>
            </div>
            <div class="space-y-2">
                <label class="block text-sm font-bold text-gray-700">البريد الإلكتروني</label>
                <div class="relative">
                    <i class="ri-mail-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400"></i>
                    <input type="email" id="edit-email" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus" required>
                </div>
            </div>
            <div class="space-y-2">
                <label class="block text-sm font-bold text-gray-700">الدور</label>
                <div class="flex gap-4 bg-gray-50 p-3 rounded-xl">
                    <label class="flex items-center gap-2 cursor-pointer">
                        <input type="radio" name="edit-role" value="user" class="w-4 h-4 text-primary">
                        <span class="text-sm">موظف</span>
                    </label>
                    <label class="flex items-center gap-2 cursor-pointer">
                        <input type="radio" name="edit-role" value="manager" class="w-4 h-4 text-primary">
                        <span class="text-sm">مدير</span>
                    </label>
                    <label class="flex items-center gap-2 cursor-pointer">
                        <input type="radio" name="edit-role" value="admin" class="w-4 h-4 text-primary">
                        <span class="text-sm">مسؤول</span>
                    </label>
                </div>
            </div>
            <div class="space-y-2">
                <label class="block text-sm font-bold text-gray-700">كلمة المرور (اتركها فارغة إذا لم ترد التغيير)</label>
                <div class="relative">
                    <i class="ri-lock-password-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400"></i>
                    <input type="password" id="edit-password" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus" placeholder="كلمة مرور جديدة">
                </div>
            </div>
            <div class="flex gap-3 pt-4">
                <button type="submit" class="flex-1 bg-gradient-to-r from-primary to-primaryDark text-white py-3.5 rounded-xl font-bold shadow-lg shadow-primary/30 hover:shadow-xl transition-all duration-300 btn-ripple flex items-center justify-center gap-2">
                    <i class="ri-save-line text-lg"></i>
                    <span>حفظ التغييرات</span>
                </button>
                <button type="button" onclick="document.getElementById('edit-user-modal').classList.add('hidden')" class="flex-1 bg-gray-100 hover:bg-gray-200 text-gray-700 py-3.5 rounded-xl font-bold transition-all duration-300 flex items-center justify-center gap-2">
                    <i class="ri-close-line text-lg"></i>
                    <span>إلغاء</span>
                </button>
            </div>
        </form>
    </div>
</div>

<!-- مودال فلترة التصدير -->
<div id="export-filter-modal" class="fixed inset-0 flex items-center justify-center z-50 modal-backdrop hidden">
    <div class="bg-white rounded-2xl p-8 w-full max-w-md mx-4 shadow-2xl border border-gray-100 animate-slide-up">
        <div class="flex justify-between items-center mb-6 pb-4 border-b border-gray-100">
            <h3 class="text-xl font-bold text-gray-800 flex items-center gap-2" id="export-filter-title">
                <i class="ri-download-cloud-2-line text-primary"></i>
                تصدير التقارير
            </h3>
            <button onclick="document.getElementById('export-filter-modal').classList.add('hidden')" class="text-gray-400 hover:text-gray-600 transition-colors p-2 hover:bg-gray-100 rounded-lg">
                <i class="ri-close-line text-2xl"></i>
            </button>
        </div>
        <form id="export-filter-form" class="space-y-5">
            <input type="hidden" id="export-type" value="">
            <div class="space-y-2">
                <label class="block text-sm font-bold text-gray-700">من تاريخ</label>
                <div class="relative">
                    <i class="ri-calendar-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400"></i>
                    <input type="date" id="export-date-from" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus">
                </div>
            </div>
            <div class="space-y-2">
                <label class="block text-sm font-bold text-gray-700">إلى تاريخ</label>
                <div class="relative">
                    <i class="ri-calendar-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400"></i>
                    <input type="date" id="export-date-to" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus">
                </div>
            </div>
            <div class="flex gap-3 pt-4">
                <button type="submit" class="flex-1 bg-gradient-to-r from-primary to-primaryDark text-white py-3.5 rounded-xl font-bold shadow-lg shadow-primary/30 hover:shadow-xl transition-all duration-300 btn-ripple flex items-center justify-center gap-2">
                    <i class="ri-download-line text-lg"></i>
                    <span>تصدير</span>
                </button>
                <button type="button" onclick="document.getElementById('export-filter-modal').classList.add('hidden')" class="flex-1 bg-gray-100 hover:bg-gray-200 text-gray-700 py-3.5 rounded-xl font-bold transition-all duration-300 flex items-center justify-center gap-2">
                    <i class="ri-close-line text-lg"></i>
                    <span>إلغاء</span>
                </button>
            </div>
        </form>
    </div>
</div>

<!-- مودال النجاح -->
<div id="success-modal" class="fixed inset-0 flex items-center justify-center z-50 modal-backdrop hidden">
    <div class="bg-white rounded-2xl p-8 w-full max-w-sm mx-4 text-center shadow-2xl border border-gray-100 animate-slide-up">
        <div class="w-20 h-20 rounded-full bg-gradient-to-br from-green-100 to-green-200 flex items-center justify-center mx-auto mb-6 shadow-lg shadow-green-500/20">
            <i class="ri-check-line text-4xl text-green-600"></i>
        </div>
        <h3 class="text-2xl font-bold text-gray-800 mb-3">تم بنجاح!</h3>
        <p id="success-msg" class="text-gray-500 mb-8 leading-relaxed"></p>
        <button onclick="this.parentElement.parentElement.classList.add('hidden')" class="w-full bg-gradient-to-r from-green-500 to-green-600 text-white py-3.5 rounded-xl font-bold shadow-lg shadow-green-500/30 hover:shadow-xl transition-all duration-300">
            حسناً
        </button>
    </div>
</div>

<!-- مودال الخطأ -->
<div id="error-modal" class="fixed inset-0 flex items-center justify-center z-50 modal-backdrop hidden">
    <div class="bg-white rounded-2xl p-8 w-full max-w-sm mx-4 text-center shadow-2xl border border-gray-100 animate-slide-up">
        <div class="w-20 h-20 rounded-full bg-gradient-to-br from-red-100 to-red-200 flex items-center justify-center mx-auto mb-6 shadow-lg shadow-red-500/20">
            <i class="ri-close-line text-4xl text-red-600"></i>
        </div>
        <h3 class="text-2xl font-bold text-gray-800 mb-3">خطأ!</h3>
        <p id="error-msg" class="text-gray-500 mb-8 leading-relaxed"></p>
        <button onclick="this.parentElement.parentElement.classList.add('hidden')" class="w-full bg-gradient-to-r from-red-500 to-red-600 text-white py-3.5 rounded-xl font-bold shadow-lg shadow-red-500/30 hover:shadow-xl transition-all duration-300">
            حسناً
        </button>
    </div>
</div>

<!-- مودال عرض المرفقات -->
<div id="attachments-modal" class="fixed inset-0 flex items-center justify-center z-50 modal-backdrop hidden">
    <div class="bg-white rounded-2xl p-6 w-full max-w-lg mx-4 shadow-2xl border border-gray-100 animate-slide-up">
        <div class="flex justify-between items-center mb-6 pb-4 border-b border-gray-100">
            <h3 class="text-xl font-bold text-gray-800 flex items-center gap-2">
                <i class="ri-attachment-2-line text-primary"></i>
                المرفقات
            </h3>
            <button onclick="document.getElementById('attachments-modal').classList.add('hidden')" class="text-gray-400 hover:text-gray-600 transition-colors p-2 hover:bg-gray-100 rounded-lg">
                <i class="ri-close-line text-2xl"></i>
            </button>
        </div>
        <div id="attachments-list" class="space-y-3 max-h-80 overflow-y-auto">
            <!-- سيتم ملؤها ديناميكياً بالروابط -->
        </div>
        <div class="mt-6 text-center">
            <button onclick="document.getElementById('attachments-modal').classList.add('hidden')" class="bg-gradient-to-r from-primary to-primaryDark text-white px-8 py-3 rounded-xl font-bold shadow-lg shadow-primary/30 hover:shadow-xl transition-all duration-300">
                إغلاق
            </button>
        </div>
    </div>
</div>

<!-- مودال إدارة رسائل المسؤول -->
<div id="messages-modal" class="fixed inset-0 flex items-center justify-center z-50 modal-backdrop hidden">
    <div class="bg-white rounded-2xl p-6 w-full max-w-2xl mx-4 max-h-[85vh] overflow-y-auto shadow-2xl border border-gray-100 animate-slide-up">
        <div class="flex justify-between items-center mb-6 pb-4 border-b border-gray-100">
            <h3 class="text-xl font-bold text-gray-800 flex items-center gap-2">
                <i class="ri-message-3-line text-primary"></i>
                إدارة رسائل المسؤول
            </h3>
            <button onclick="closeMessagesModal()" class="text-gray-400 hover:text-gray-600 transition-colors p-2 hover:bg-gray-100 rounded-lg">
                <i class="ri-close-line text-2xl"></i>
            </button>
        </div>
        <p class="text-sm text-gray-500 mb-4 bg-gray-50 p-3 rounded-lg">أدخل الرسائل التي تريد عرضها في الشريط المتحرك للموظفين، كل رسالة في سطر منفصل.</p>
        <textarea id="admin-messages-textarea" rows="8" class="w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus resize-none mb-5" placeholder="الرسالة الأولى&#10;الرسالة الثانية&#10;الرسالة الثالثة"></textarea>
        
        <div class="flex items-center gap-4 mb-6 bg-gray-50 p-4 rounded-xl">
            <label class="text-sm font-bold text-gray-700 whitespace-nowrap">سرعة الحركة (ثانية):</label>
            <input type="number" id="marquee-speed" min="5" max="100" value="25" class="w-24 px-3 py-2 border-2 border-gray-200 rounded-lg focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all">
            <button onclick="updateMarqueeSpeed()" class="bg-gray-200 hover:bg-gray-300 px-4 py-2 rounded-lg text-sm font-bold transition-all">تطبيق</button>
        </div>

        <div class="flex gap-3 pt-4 border-t border-gray-100">
            <button onclick="saveMessages()" class="flex-1 bg-gradient-to-r from-primary to-primaryDark text-white py-3.5 rounded-xl font-bold shadow-lg shadow-primary/30 hover:shadow-xl transition-all duration-300 btn-ripple flex items-center justify-center gap-2">
                <i class="ri-save-line text-lg"></i>
                <span>حفظ التغييرات</span>
            </button>
            <button onclick="closeMessagesModal()" class="flex-1 bg-gray-100 hover:bg-gray-200 text-gray-700 py-3.5 rounded-xl font-bold transition-all duration-300 flex items-center justify-center gap-2">
                <i class="ri-close-line text-lg"></i>
                <span>إلغاء</span>
            </button>
        </div>
    </div>
</div>

<!-- مودال رفع قائمة الأسعار -->
<div id="price-list-modal" class="fixed inset-0 flex items-center justify-center z-50 modal-backdrop hidden">
    <div class="bg-white rounded-2xl p-6 w-full max-w-md mx-4 shadow-2xl border border-gray-100 animate-slide-up">
        <div class="flex justify-between items-center mb-6 pb-4 border-b border-gray-100">
            <h3 class="text-xl font-bold text-gray-800 flex items-center gap-2">
                <i class="ri-price-tag-3-line text-red-500"></i>
                رفع قائمة الأسعار
            </h3>
            <button onclick="closePriceListModal()" class="text-gray-400 hover:text-gray-600 transition-colors p-2 hover:bg-gray-100 rounded-lg">
                <i class="ri-close-line text-2xl"></i>
            </button>
        </div>
        <form id="price-list-form" class="space-y-5">
            <div class="space-y-2">
                <label class="block text-sm font-bold text-gray-700">نوع المستند</label>
                <div class="relative">
                    <i class="ri-file-type-line absolute right-4 top-1/2 -translate-y-1/2 text-gray-400"></i>
                    <select id="price-list-type" class="w-full pr-12 pl-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all input-focus bg-gray-50/50 appearance-none">
                        <option value="image">صورة</option>
                        <option value="pdf">PDF</option>
                        <option value="word">Word</option>
                    </select>
                    <i class="ri-arrow-down-s-line absolute left-4 top-1/2 -translate-y-1/2 text-gray-400 text-lg pointer-events-none"></i>
                </div>
            </div>
            <div class="space-y-2">
                <label class="block text-sm font-bold text-gray-700">الملف</label>
                <input type="file" id="price-list-file" accept=".jpg,.jpeg,.png,.pdf,.doc,.docx" class="file-input-primary w-full px-4 py-3 border-2 border-dashed border-gray-300 rounded-xl hover:border-primary transition-colors bg-gray-50/50" required>
            </div>
            <div class="flex gap-3 pt-4">
                <button type="button" onclick="uploadPriceList()" class="flex-1 bg-gradient-to-r from-primary to-primaryDark text-white py-3.5 rounded-xl font-bold shadow-lg shadow-primary/30 hover:shadow-xl transition-all duration-300 btn-ripple flex items-center justify-center gap-2">
                    <i class="ri-upload-cloud-2-line text-lg"></i>
                    <span>رفع</span>
                </button>
                <button type="button" onclick="closePriceListModal()" class="flex-1 bg-gray-100 hover:bg-gray-200 text-gray-700 py-3.5 rounded-xl font-bold transition-all duration-300 flex items-center justify-center gap-2">
                    <i class="ri-close-line text-lg"></i>
                    <span>إلغاء</span>
                </button>
            </div>
        </form>
        <div id="price-list-link-container" class="mt-5 p-4 bg-gray-50 rounded-xl hidden">
            <p class="text-sm text-gray-600 mb-2 font-bold">الرابط الحالي:</p>
            <a id="price-list-link" href="#" target="_blank" class="text-primary hover:text-primaryDark hover:underline break-all text-sm font-medium"></a>
        </div>
    </div>
</div>

<!-- مودال عرض المستند للطباعة -->
<div id="preview-modal" class="fixed inset-0 flex items-center justify-center z-50 modal-backdrop hidden">
    <div class="bg-white rounded-2xl p-6 w-full max-w-5xl mx-4 max-h-[90vh] overflow-y-auto shadow-2xl border border-gray-100 animate-slide-up">
        <div class="flex justify-between items-center mb-6 pb-4 border-b border-gray-100 sticky top-0 bg-white z-10">
            <h3 id="preview-modal-title" class="text-xl font-bold text-gray-800 flex items-center gap-2">
                <i class="ri-file-text-line text-primary"></i>
                تفاصيل المستند
            </h3>
            <button onclick="closePreviewModal()" class="text-gray-400 hover:text-gray-600 transition-colors p-2 hover:bg-gray-100 rounded-lg">
                <i class="ri-close-line text-2xl"></i>
            </button>
        </div>
        <div id="preview-content" class="space-y-4"></div>
        <div class="flex justify-center gap-4 mt-8 pt-6 border-t border-gray-100 sticky bottom-0 bg-white">
            <button onclick="printPreview()" class="bg-gradient-to-r from-primary to-primaryDark text-white px-8 py-3.5 rounded-xl font-bold shadow-lg shadow-primary/30 hover:shadow-xl transition-all duration-300 flex items-center gap-2">
                <i class="ri-printer-line text-lg"></i>
                <span>طباعة</span>
            </button>
            <button onclick="closePreviewModal()" class="bg-gray-100 hover:bg-gray-200 text-gray-700 px-8 py-3.5 rounded-xl font-bold transition-all duration-300 flex items-center gap-2">
                <i class="ri-close-line text-lg"></i>
                <span>إغلاق</span>
            </button>
        </div>
    </div>
</div>

<!-- مودال المستندات (مبني على) -->
<div id="based-on-modal" class="fixed inset-0 flex items-center justify-center z-50 modal-backdrop hidden">
    <div class="bg-white rounded-2xl p-6 w-full max-w-5xl mx-4 max-h-[85vh] overflow-y-auto shadow-2xl border border-gray-100 animate-slide-up">
        <div class="flex justify-between items-center mb-6 pb-4 border-b border-gray-100">
            <h3 class="text-xl font-bold text-gray-800 flex items-center gap-2">
                <i class="ri-stackshare-line text-amber-500"></i>
                اختيار مستند
            </h3>
            <button onclick="closeBasedOnModal()" class="text-gray-400 hover:text-gray-600 transition-colors p-2 hover:bg-gray-100 rounded-lg">
                <i class="ri-close-line text-2xl"></i>
            </button>
        </div>
        <div class="mb-4">
            <p class="text-sm text-gray-600">اختر أحد المستندات لإضافته كنشاط يومي:</p>
        </div>
        <div id="documents-list" class="flex overflow-x-auto gap-4 pb-4" style="scrollbar-width: thin;"></div>
    </div>
</div>



<script>
      // ============================================================================
// ملف الجافاسكريبت الرئيسي - Hyma Plastic Sales System (نسخة محسنة للأداء)
// ============================================================================

// ═══════════════════════════════════════════════════════════════════════════
// القسم الأول: المتغيرات العامة والإعدادات (محسنة بالكامل)
// ═══════════════════════════════════════════════════════════════════════════

const SHEET_CONFIG = {
    SALES_SHEET_NAME: 'تقارير المبيعات',
    COMPLAINTS_SHEET_NAME: 'شكاوى العملاء',
    QUOTES_SHEET_NAME: 'عروض الأسعار',
    USERS_SHEET_NAME: 'Hyma_Users',
    CUSTOMERS_SHEET_NAME: 'العملاء',
    VISITS_SHEET_NAME: 'زيارات العملاء',
    ACTIVITIES_SHEET_NAME: 'النشاط اليومي',
    PLANS_SHEET_NAME: 'الخطة_الاسبوعية',
    COLLECTIONS_SHEET_NAME: 'التحصيلات',
    PENDING_USERS_SHEET: 'طلبات_المستخدمين',
    ITEMS_SHEET_NAME: 'الأصناف',
    WEB_APP_URL: 'https://script.google.com/macros/s/AKfycbxcflYv-Vg6tCsp28uKT1ofZ8m9LkHCRR2RN6RAyo9_qxfFG38zLMcOUjTLf_AOO_Qn/exec'
};

// ═══════════════════════════════════════════════════════════════════════════
// نظام التخزين المؤقت المتقدم (Cache System) - جديد للأداء
// ═══════════════════════════════════════════════════════════════════════════
const appCache = {
    data: {
        sales: [],
        complaints: [],
        quotes: [],
        users: [],
        customers: [],
        visits: [],
        activities: [],
        plans: [],
        collections: [],
        pendingUsers: [],
        items: []
    },
    timestamp: 0,
    CACHE_DURATION: 5 * 60 * 1000, // 5 دقائق
    pendingRequests: new Map(),
    
    get(key) {
        if (Date.now() - this.timestamp > this.CACHE_DURATION) return null;
        return this.data[key] || null;
    },
    
    set(key, value) {
        this.data[key] = value;
        this.timestamp = Date.now();
    },
    
    clear() {
        this.timestamp = 0;
    }
};

// خرائط البحث السريع (Maps للوصول O(1))
const customersMap = new Map();
const itemsMap = new Map();
const fieldMapCache = new Map();
const dateFormatCache = new Map();
const docTemplateCache = new Map();
const escapeHtmlCache = new Map();
const idCounters = new Map();
const pendingSaves = new Map();
const searchableDropdownsMap = new WeakMap();

// متغيرات الحالة
let currentUser = null;
let isSavingCustomer = false;
let isSavingPlan = false;
let isSavingVisit = false;
let isSavingActivity = false;
let isSavingQuote = false;
let isSavingSale = false;
let isSavingComplaint = false;
let isSavingCollection = false;
let isEditingSale = false;
let editingSaleId = null;
let isEditingQuote = false;
let editingQuoteId = null;
let isEditingCustomer = false;
let editingCustomerId = null;
let adminMessages = [];
let originalCustomerStatus = '';
let dropdownsInitialized = false;

// ═══════════════════════════════════════════════════════════════════════════
// القسم الثاني: دوال المساعدة الأساسية (محسنة للأداء)
// ═══════════════════════════════════════════════════════════════════════════

// Debounce للأحداث المتكررة
function debounce(func, wait) {
    let timeout;
    return function executedFunction(...args) {
        const later = () => {
            clearTimeout(timeout);
            func(...args);
        };
        clearTimeout(timeout);
        timeout = setTimeout(later, wait);
    };
}

// Throttle للأحداث المستمرة
function throttle(func, limit) {
    let inThrottle;
    return function(...args) {
        if (!inThrottle) {
            func.apply(this, args);
            inThrottle = true;
            setTimeout(() => inThrottle = false, limit);
        }
    };
}

// تحديث خرائط البحث السريع
function updateSearchMaps() {
    customersMap.clear();
    appCache.data.customers.forEach(c => {
        const id = getSafeValue(c, 'معرف');
        if (id) customersMap.set(id, c);
    });
    
    itemsMap.clear();
    appCache.data.items.forEach(item => {
        const code = getSafeValue(item, 'الكود') || getSafeValue(item, 'code');
        if (code) itemsMap.set(code, item);
    });
}

function getItemsOptions(selectedCode = '') {
    if (!appCache.data.items?.length) {
        return '<option value="">لا توجد أصناف</option>';
    }
    
    let options = '<option value="">-- اختر كود الصنف --</option>';
    
    appCache.data.items.forEach(item => {
        const code = getSafeValue(item, 'الكود') || getSafeValue(item, 'code') || '';
        const name = getSafeValue(item, 'الاسم') || getSafeValue(item, 'name') || '';
        if (code) {
            const selected = (code === selectedCode) ? 'selected' : '';
            options += `<option value="${code.replace(/"/g, '&quot;')}" data-name="${name.replace(/"/g, '&quot;')}" ${selected}>${code} - ${name}</option>`;
        }
    });
    
    return options;
}

function getCurrentDateTime() {
    const now = new Date();
    return `${now.getFullYear()}-${String(now.getMonth() + 1).padStart(2, '0')}-${String(now.getDate()).padStart(2, '0')} ${String(now.getHours()).padStart(2, '0')}:${String(now.getMinutes()).padStart(2, '0')}`;
}

function formatDate(dateValue, noTime = false) {
    if (!dateValue) return '-';
    
    const cacheKey = `${dateValue}-${noTime}`;
    if (dateFormatCache.has(cacheKey)) {
        return dateFormatCache.get(cacheKey);
    }
    
    try {
        const date = new Date(dateValue);
        if (isNaN(date.getTime())) {
            dateFormatCache.set(cacheKey, dateValue);
            return dateValue;
        }
        
        const day = String(date.getDate()).padStart(2, '0');
        const month = String(date.getMonth() + 1).padStart(2, '0');
        const year = date.getFullYear();
        const dateStr = `${day}-${month}-${year}`;
        
        if (noTime) {
            dateFormatCache.set(cacheKey, dateStr);
            return dateStr;
        }
        
        let hours = date.getHours();
        const minutes = String(date.getMinutes()).padStart(2, '0');
        const ampm = hours >= 12 ? 'م' : 'ص';
        hours = hours % 12 || 12;
        
        const result = `${dateStr} ${String(hours).padStart(2, '0')}:${minutes} ${ampm}`;
        dateFormatCache.set(cacheKey, result);
        return result;
        
    } catch (e) {
        dateFormatCache.set(cacheKey, dateValue);
        return dateValue;
    }
}

// تنظيف الذاكرة المؤقتة للتواريخ كل ساعة
setInterval(() => dateFormatCache.clear(), 3600000);

function formatTimeOnly(timeValue) {
    if (!timeValue) return '-';
    if (typeof timeValue === 'string' && /^\d{2}:\d{2}$/.test(timeValue)) return timeValue;
    if (typeof timeValue === 'string' && timeValue.includes(' ')) return timeValue.split(' ')[1];
    try {
        let d = new Date(timeValue);
        if (!isNaN(d)) {
            return String(d.getHours()).padStart(2, '0') + ':' + String(d.getMinutes()).padStart(2, '0');
        }
    } catch {}
    return timeValue;
}

function getSafeValue(row, field) {
    if (!row || typeof row !== 'object') return '';
    
    if (row[field] !== undefined && row[field] !== null) {
        return row[field];
    }
    
    if (!fieldMapCache.has(field)) {
        const fieldMap = {
            'الموظف': ['الموظف','اسم_المستخدم','username','User','user','اسم المستخدم','المستخدم','اسم الموظف','employee'],
            'التاريخ': ['التاريخ','Date','date','تاريخ'],
            'معرف': ['معرف','id','ID'],
            'اسم_العميل': ['اسم_العميل', 'اسم العميل', 'العميل', 'client', 'Client', 'customer', 'Customer', 'الاسم'],
            'الحالة': ['الحالة','Status','status','حالة التقرير','الوضع','حالة'],
            'الملاحظات': ['الملاحظات','Notes','notes','ملاحظات','تعليقات'],
            'النوع': ['النوع','Type','type','نوع الشكوى','التصنيف'],
            'رقم_الهاتف': ['رقم_الهاتف','Phone','phone','هاتف','رقم الهاتف','الجوال'],
            'البريد_الإلكتروني': ['البريد_الإلكتروني','Email','email','البريد','بريد إلكتروني','الإيميل'],
            'العنوان': ['العنوان','Address','address'],
            'الوصف': ['الوصف','Description','description','تفاصيل','شرح'],
            'مكان_التصنيع': ['مكان_التصنيع','مكان التصنيع','ManufacturingLocation'],
            'طريقة_السداد': ['طريقة_السداد','طريقة السداد','PaymentMethod'],
            'مكان_التسليم': ['مكان_التسليم','مكان التسليم','DeliveryPlace'],
            'تفاصيل_الأصناف': ['تفاصيل_الأصناف','ItemsDetails','items_details'],
            'سبب_الرفض': ['سبب_الرفض','RejectionReason','rejection_reason','سبب الرفض'],
            'المرفق': ['المرفق', 'المرفقات', 'attachment', 'attachments', 'Attachment', 'Attachments', 'الملف', 'الملفات'],
        };
        fieldMapCache.set(field, fieldMap[field] || [field]);
    }
    
    const possible = fieldMapCache.get(field);
    
    for (let key in row) {
        const trimmedKey = String(key).trim();
        for (let name of possible) {
            if (trimmedKey === name) {
                let val = row[key];
                return val !== undefined && val !== null ? val : '';
            }
        }
    }
    
    return '';
}

function usernameMatches(itemUsername, currentUsername) {
    if (!itemUsername || !currentUsername) return false;
    return String(itemUsername).trim().toLowerCase() === String(currentUsername).trim().toLowerCase();
}

function objectToFormData(obj) {
    const fd = new URLSearchParams();
    for (let k in obj) {
        if (obj.hasOwnProperty(k)) {
            let val = obj[k];
            if (Array.isArray(val)) val = JSON.stringify(val);
            if (val !== undefined && val !== null) fd.append(k, val);
        }
    }
    return fd;
}

async function sendRequest(data) {
    const cacheKey = JSON.stringify(data);
    
    if (appCache.pendingRequests.has(cacheKey)) {
        return await appCache.pendingRequests.get(cacheKey);
    }
    
    const fd = objectToFormData(data);
    
    const promise = (async () => {
        try {
            const url = SHEET_CONFIG.WEB_APP_URL + '?t=' + Date.now();
            const res = await fetch(url, { method: 'POST', body: fd });
            return await res.json();
        } catch (e) {
            console.error('خطأ في الإرسال:', e);
            throw e;
        } finally {
            appCache.pendingRequests.delete(cacheKey);
        }
    })();
    
    appCache.pendingRequests.set(cacheKey, promise);
    return await promise;
}

function numberToArabicWords(num) {
    if (!num || num === 0) return 'صفر';
    const units = ['', 'واحد', 'اثنان', 'ثلاثة', 'أربعة', 'خمسة', 'ستة', 'سبعة', 'ثمانية', 'تسعة', 'عشرة', 'أحد عشر', 'اثنا عشر', 'ثلاثة عشر', 'أربعة عشر', 'خمسة عشر', 'ستة عشر', 'سبعة عشر', 'ثمانية عشر', 'تسعة عشر'];
    const tens = ['', '', 'عشرون', 'ثلاثون', 'أربعون', 'خمسون', 'ستون', 'سبعون', 'ثمانون', 'تسعون'];
    const hundreds = ['', 'مائة', 'مائتان', 'ثلاثمائة', 'أربعمائة', 'خمسمائة', 'ستمائة', 'سبعمائة', 'ثمانمائة', 'تسعمائة'];
    
    function convertThreeDigits(n) {
        let h = Math.floor(n / 100);
        let rest = n % 100;
        let result = '';
        if (h > 0) result += hundreds[h];
        if (rest > 0) {
            if (result !== '') result += ' و ';
            if (rest < 20) result += units[rest];
            else {
                let ten = Math.floor(rest / 10);
                let unit = rest % 10;
                if (unit > 0) result += units[unit] + ' و ' + tens[ten];
                else result += tens[ten];
            }
        }
        return result;
    }
    
    let parts = [];
    let millions = Math.floor(num / 1000000);
    let thousands = Math.floor((num % 1000000) / 1000);
    let remainder = num % 1000;
    
    if (millions > 0) parts.push(convertThreeDigits(millions) + (millions === 1 ? ' مليون' : ' ملايين'));
    if (thousands > 0) parts.push(convertThreeDigits(thousands) + (thousands === 1 ? ' ألف' : ' آلاف'));
    if (remainder > 0) parts.push(convertThreeDigits(remainder));
    
    return parts.join(' و ') + ' جنيهاً مصرياً فقط لا غير';
}

function makeSearchableDropdown(selectElement, clientList) {
    if (!selectElement || searchableDropdownsMap.has(selectElement)) return;
    
    selectElement.style.display = 'none';
    
    const container = document.createElement('div');
    container.className = 'searchable-wrapper relative w-full';
    
    const searchInput = document.createElement('input');
    searchInput.type = 'text';
    searchInput.placeholder = 'ابحث عن عميل...';
    searchInput.className = 'w-full px-4 py-3.5 border-2 border-gray-200 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all';
    searchInput.autocomplete = 'off';
    
    const suggestionsDiv = document.createElement('div');
    suggestionsDiv.className = 'dropdown-suggestions absolute z-50 w-full bg-white border border-gray-200 rounded-b-xl max-h-60 overflow-y-auto hidden';
    
    container.appendChild(searchInput);
    container.appendChild(suggestionsDiv);
    selectElement.parentNode.insertBefore(container, selectElement.nextSibling);
    
    searchableDropdownsMap.set(selectElement, { container, searchInput, suggestionsDiv });
    
    const updateSuggestions = debounce(() => {
        const term = searchInput.value.trim().toLowerCase();
        let filtered = term ? clientList.filter(c => c.name.toLowerCase().includes(term)) : clientList;
        
        suggestionsDiv.innerHTML = '';
        
        if (filtered.length === 0) {
            suggestionsDiv.innerHTML = '<div class="px-4 py-3 text-gray-500">لا توجد نتائج</div>';
        } else {
            const fragment = document.createDocumentFragment();
            filtered.forEach(client => {
                const item = document.createElement('div');
                item.textContent = client.name;
                item.className = 'px-4 py-3 hover:bg-primary/10 cursor-pointer transition-colors';
                item.onclick = () => {
                    selectElement.value = client.name;
                    searchInput.value = client.name;
                    suggestionsDiv.classList.add('hidden');
                    
                    const page = document.querySelector('[id$="-page"]:not(.hidden)')?.id;
                    if (page === 'add-complaint-page') {
                        const emailField = document.getElementById('complaint-email');
                        const phoneField = document.getElementById('complaint-phone');
                        if (emailField) emailField.value = client.email || '';
                        if (phoneField) phoneField.value = client.phone || '';
                    }
                };
                fragment.appendChild(item);
            });
            suggestionsDiv.appendChild(fragment);
        }
        suggestionsDiv.classList.remove('hidden');
    }, 150);
    
    searchInput.addEventListener('focus', updateSuggestions);
    searchInput.addEventListener('input', updateSuggestions);
    
    document.addEventListener('click', (e) => {
        if (!container.contains(e.target)) suggestionsDiv.classList.add('hidden');
    });
    
    if (selectElement.value) {
        const selected = clientList.find(c => c.name === selectElement.value);
        searchInput.value = selected ? selected.name : selectElement.value;
    }
}

function initSearchableDropdowns() {
    if (!currentUser || dropdownsInitialized) return;
    
    let myCustomers = [];
    
    if (currentUser.role === 'admin' || currentUser.role === 'manager') {
        myCustomers = appCache.data.customers.filter(c => 
            getSafeValue(c, 'الحالة') === 'معتمد'
        ).map(c => ({
            name: getSafeValue(c, 'اسم_العميل') || getSafeValue(c, 'اسم العميل'),
            email: getSafeValue(c, 'البريد_الإلكتروني') || '',
            phone: getSafeValue(c, 'رقم_الهاتف') || ''
        }));
    } else {
        myCustomers = appCache.data.customers.filter(c => 
            usernameMatches(getSafeValue(c, 'الموظف'), currentUser.username) && 
            getSafeValue(c, 'الحالة') === 'معتمد'
        ).map(c => ({
            name: getSafeValue(c, 'اسم_العميل') || getSafeValue(c, 'اسم العميل'),
            email: getSafeValue(c, 'البريد_الإلكتروني') || '',
            phone: getSafeValue(c, 'رقم_الهاتف') || ''
        }));
    }
    
    const selectIds = ['sale-client-select', 'quote-client-select', 'complaint-client-select', 'visit-client-select', 'collection-client-select'];
    
    selectIds.forEach(id => {
        const selectEl = document.getElementById(id);
        if (selectEl && !searchableDropdownsMap.has(selectEl)) {
            makeSearchableDropdown(selectEl, myCustomers);
        }
    });
    
    dropdownsInitialized = true;
}

// ═══════════════════════════════════════════════════════════════════════════
// القسم الثالث: قوالب المستندات (محسنة بالتخزين المؤقت)
// ═══════════════════════════════════════════════════════════════════════════

function getDocHeader(title, docNumber, date, employee) {
    return `
        <div class="doc-header" style="display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid #198a11; padding-bottom: 10px; margin-bottom: 20px;">
            <!-- الشعار واسم الشركة على اليمين -->
            <div class="doc-header-right" style="text-align: right;">
                <div style="display: flex; align-items: center; gap: 10px;">
                    <img src="https://g.top4top.io/p_3708dgdoj1.png" alt="Hyma Plastic" style="height: 50px;">
                    <div>
                        <div style="font-weight: bold; font-size: 16px;">Hyma Plastic</div>
                    </div>
                </div>
            </div>
            <!-- عنوان المستند في المنتصف -->
            <div class="doc-header-center" style="text-align: center;">
                <h1 style="margin: 0; font-size: 24px; color: #198a11;">${title}</h1>
            </div>
            <!-- البيانات (رقم المستند، التاريخ، الموظف) على اليسار -->
            <div class="doc-header-left" style="text-align: left;">
                ${docNumber ? `<div><strong>رقم المستند:</strong> ${docNumber}</div>` : ''}
                ${date ? `<div><strong>التاريخ:</strong> ${date}</div>` : ''}
                ${employee ? `<div><strong>مسئول المبيعات:</strong> ${employee}</div>` : ''}
            </div>
        </div>
    `;
    
    docTemplateCache.set(cacheKey, html);
    return html;
}

function getDocFooter() {
    return `
        <div class="doc-footer" style="border-top: 2px solid #198a11; margin-top: 20px; padding-top: 15px; text-align: center; font-size: 11px; color: #666;">
            <div>www.Hyma-Plastic.com </div>
            <div>sales@hyma-plastic.com | export@hyma-plastic.com | office@hyma-plastic.com</div>
            <div>العنوان: 22 حدائق العبور - ش صالح سالم - مدينة نصر - القاهرة - مصر 11811 | ص.ب 8007 مدينة نصر</div>
            <div>ت: 24011626 | فاكس: 24011627 </div>
            <div>مصنع: المنصورية، امبابة، جيزة | ت: 38900726 - 38900728</div>
        </div>
    `;
}

function getDocSignatures() {
    return `
        <div class="doc-signatures">
            <div class="doc-signature-box">
                <div class="doc-signature-line"></div>
            </div>
            <div class="doc-signature-box">
                <div class="doc-signature-line"></div>
            </div>
            <div class="doc-signature-box">
                <div class="doc-signature-line"></div>
            </div>
        </div>
    `;
}

function generateSalesOrderHTML(sale) {
    const docNumber = sale['معرف'] || sale['id'] || '';
    let formattedDate = formatDate(sale['التاريخ'] || sale['date'] || '', true);
    const employee = sale['الموظف'] || sale['employee'] || '';
    const customer = sale['العميل'] || sale['client'] || '';
    const customerCode = sale['كود_العميل'] || sale['clientCode'] || '';
    const deliveryPlace = sale['مكان_التسليم'] || sale['deliveryPlace'] || '';
    const manufacturingLocation = sale['مكان_التصنيع'] || sale['manufacturingLocation'] || '';
    const paymentMethod = sale['طريقة_السداد'] || sale['paymentMethod'] || '';
    const terms = sale['الشروط_والأحكام'] || sale['terms'] || '';
    const notes = sale['ملاحظات'] || sale['notes'] || '';
    
    let subtotal = parseFloat(sale['الإجمالي_قبل_الضريبة'] || sale['subtotal'] || 0);
    let tax = parseFloat(sale['الضريبة'] || sale['tax'] || 0);
    let total = parseFloat(sale['الإجمالي_الكلي'] || sale['total'] || 0);
    
    let items = [];
    try {
        items = JSON.parse(sale['تفاصيل_الأصناف'] || sale['itemsDetails'] || '[]');
        if (!Array.isArray(items)) items = [];
    } catch(e) { items = []; }
    
    const formatCurrency = (num) => {
        if (!num || isNaN(num)) return '0.00';
        return parseFloat(num).toLocaleString('ar-EG', { minimumFractionDigits: 2, maximumFractionDigits: 2 });
    };
    
    const totalInWords = numberToArabicWords(Math.floor(total));
    
    let tableRows = items.map((item, index) => {
        const qty = parseFloat(item.qty) || 0;
        const unitPrice = parseFloat(item.unitPrice) || 0;
        const discount = parseFloat(item.discount) || 0;
        const totalAfterDiscount = parseFloat(item.total) || (qty * unitPrice * (1 - discount/100));
        
        return `
            <tr>
                <td style="padding: 8px; border: 1px solid #333; text-align: center;">${index + 1}</td>
                <td style="padding: 8px; border: 1px solid #333; text-align: center;">${item.code || ''}</td>
                <td style="padding: 8px; border: 1px solid #333; text-align: right;">${item.name || ''}</td>
                <td style="padding: 8px; border: 1px solid #333; text-align: center;">${qty}</td>
                <td style="padding: 8px; border: 1px solid #333; text-align: center;">${item.unit || ''}</td>
                <td style="padding: 8px; border: 1px solid #333; text-align: right;">${formatCurrency(unitPrice)}</td>
                <td style="padding: 8px; border: 1px solid #333; text-align: center;">${discount > 0 ? discount + '%' : '0.00'}</td>
                <td style="padding: 8px; border: 1px solid #333; text-align: right;">${formatCurrency(totalAfterDiscount)}</td>
            </tr>
        `;
    }).join('') || '<tr><td colspan="8" style="padding: 20px; text-align: center; border: 1px solid #333;">لا توجد أصناف</td></tr>';
    
    return `
        <div class="doc-container">
            ${getDocHeader('أمر بيع', docNumber, formattedDate, employee)}
            
            <div class="doc-section">
                <div class="row">
                    <div class="col-6">
                        ${customer ? `<div class="doc-info-row"><span class="doc-info-label">العميل:</span> ${customer}</div>` : ''}
                        ${customerCode ? `<div class="doc-info-row"><span class="doc-info-label">كود العميل:</span> ${customerCode}</div>` : ''}
                    </div>
                    <div class="col-6">
                        ${deliveryPlace ? `<div class="doc-info-row"><span class="doc-info-label">عنوان التسليم:</span> ${deliveryPlace}</div>` : ''}
                        ${manufacturingLocation ? `<div class="doc-info-row"><span class="doc-info-label">مكان التصنيع:</span> ${manufacturingLocation}</div>` : ''}
                        ${paymentMethod ? `<div class="doc-info-row"><span class="doc-info-label">طريقة السداد:</span> ${paymentMethod}</div>` : ''}
                    </div>
                </div>
            </div>

            <table class="doc-table">
                <thead>
                    <tr>
                        <th style="width: 5%;">م</th>
                        <th style="width: 12%;">كود الصنف</th>
                        <th style="width: 30%;">وصف الصنف</th>
                        <th style="width: 8%;">الكمية</th>
                        <th style="width: 8%;">وحدة</th>
                        <th style="width: 10%;">السعر</th>
                        <th style="width: 8%;">الخصم %</th>
                        <th style="width: 12%;">الإجمالي</th>
                    </tr>
                </thead>
                <tbody>${tableRows}</tbody>
            </table>

            ${(subtotal > 0 || tax > 0 || total > 0) ? `
            <div class="doc-totals">
                <table class="doc-totals-table">
                    ${subtotal > 0 ? `
                    <tr>
                        <td class="label">الإجمالي قبل الضريبة:</td>
                        <td class="value">${formatCurrency(subtotal)}</td>
                    </tr>` : ''}
                    ${tax > 0 ? `
                    <tr>
                        <td class="label">ضريبة القيمة المضافة (14%):</td>
                        <td class="value">${formatCurrency(tax)}</td>
                    </tr>` : ''}
                    ${total > 0 ? `
                    <tr class="doc-grand-total">
                        <td class="label">الإجمالي الكلي:</td>
                        <td class="value" style="color: #198a11;">${formatCurrency(total)}</td>
                    </tr>` : ''}
                </table>
            </div>
            ` : ''}

            ${total > 0 ? `<div class="doc-amount-words">فقط ${totalInWords}</div>` : ''}

            ${terms ? `
            <div class="doc-terms">
                <div class="doc-section-title">الشروط والأحكام:</div>
                <div style="white-space: pre-line; font-size: 11px;">${terms}</div>
            </div>` : ''}

            ${notes ? `
            <div class="doc-notes">
                <div class="doc-section-title">ملاحظات:</div>
                <div style="font-size: 11px;">${notes}</div>
            </div>` : ''}

            ${getDocSignatures()}
            ${getDocFooter()}
        </div>
    `;
}

function generateQuoteHTML(quote) {
    const docNumber = getSafeValue(quote, 'معرف') || '';
    const formattedDate = formatDate(getSafeValue(quote, 'التاريخ'), true);
    const employee = getSafeValue(quote, 'الموظف') || '';
    const customer = getSafeValue(quote, 'العميل') || '';
    const paymentMethod = getSafeValue(quote, 'طريقة_السداد') || '';
    const validity = getSafeValue(quote, 'مدة_العرض') || '30 يوم';
    const deliveryPlace = getSafeValue(quote, 'مكان_التسليم') || '';
    const notes = getSafeValue(quote, 'الملاحظات') || '';
    const taxType = getSafeValue(quote, 'نوع_الضريبة') || 'exclusive';
    
    let subtotal = parseFloat(getSafeValue(quote, 'الإجمالي_قبل_الضريبة') || quote['الإجمالي_قبل_الضريبة'] || 0);
    let tax = parseFloat(getSafeValue(quote, 'الضريبة') || quote['الضريبة'] || 0);
    let total = parseFloat(getSafeValue(quote, 'الإجمالي_الكلي') || quote['الإجمالي_الكلي'] || 0);
    
    let items = [];
    try {
        const itemsRaw = getSafeValue(quote, 'تفاصيل_الأصناف') || quote['تفاصيل_الأصناف'] || '[]';
        items = JSON.parse(itemsRaw);
        if (!Array.isArray(items)) items = [];
    } catch(e) {
        console.error('خطأ في تحليل الأصناف:', e);
        items = [];
    }
    
    if (subtotal === 0 && items.length > 0) {
        subtotal = items.reduce((sum, item) => sum + (parseFloat(item.qty) || 0) * (parseFloat(item.unitPrice) || 0), 0);
        if (taxType === 'exclusive') {
            tax = subtotal * 0.14;
            total = subtotal + tax;
        } else {
            total = subtotal;
            tax = total - (total / 1.14);
            subtotal = total - tax;
        }
    }
    
    const formatCurrency = (num) => {
        if (num === undefined || num === null || isNaN(num)) return '0.00';
        return parseFloat(num).toLocaleString('ar-EG', { minimumFractionDigits: 2, maximumFractionDigits: 2 });
    };
    
    const totalInWords = (typeof numberToArabicWords === 'function') ? numberToArabicWords(Math.floor(total)) : '';
    const taxTypeText = (taxType === 'inclusive') ? 'شامل الضريبة' : 'غير شامل الضريبة';
    
    let tableRows = '';
    if (items.length === 0) {
        tableRows = '<tr><td colspan="6" style="padding: 20px; text-align: center; border: 1px solid #333;">لا توجد أصناف</td></tr>';
    } else {
        tableRows = items.map((item, index) => {
            const qty = parseFloat(item.qty) || 0;
            const unitPrice = parseFloat(item.unitPrice) || 0;
            const itemTotal = parseFloat(item.total) || (qty * unitPrice);
            return `
                <tr>
                    <td style="padding: 8px; border: 1px solid #333; text-align: center;">${index + 1}</td>
                    <td style="padding: 8px; border: 1px solid #333; text-align: center;">${escapeHtml(item.code || '')}</td>
                    <td style="padding: 8px; border: 1px solid #333; text-align: right;">${escapeHtml(item.name || '')}</td>
                    <td style="padding: 8px; border: 1px solid #333; text-align: center;">${qty} ${item.unit ? escapeHtml(item.unit) : ''}</td>
                    <td style="padding: 8px; border: 1px solid #333; text-align: left;">${formatCurrency(unitPrice)} ج.م</td>
                    <td style="padding: 8px; border: 1px solid #333; text-align: left;">${formatCurrency(itemTotal)} ج.م</td>
                </tr>
            `;
        }).join('');
    }
    
    return `
        <div class="doc-container">
            ${getDocHeader('عرض سعر', docNumber, formattedDate, employee)}
            
            <div class="doc-section">
                <div style="display: flex; justify-content: space-between; margin-bottom: 15px; flex-wrap: wrap;">
                    <div style="width: 48%; min-width: 200px;">
                        <div class="doc-info-row"><strong>العميل:</strong> ${escapeHtml(customer) || '-'}</div>
                        ${paymentMethod ? `<div class="doc-info-row"><strong>طريقة السداد:</strong> ${escapeHtml(paymentMethod)}</div>` : ''}
                    </div>
                    <div style="width: 48%; min-width: 200px;">
                        ${deliveryPlace ? `<div class="doc-info-row"><strong>مكان التسليم:</strong> ${escapeHtml(deliveryPlace)}</div>` : ''}
                        <div class="doc-info-row"><strong>مدة العرض:</strong> ${escapeHtml(validity)}</div>
                        <div class="doc-info-row"><strong>نوع الضريبة:</strong> ${taxTypeText}</div>
                    </div>
                </div>
            </div>

            <table style="width:100%; border-collapse: collapse; margin: 15px 0;">
                <thead>
                    <tr style="background-color: #f2f2f2;">
                        <th style="padding: 8px; border: 1px solid #333; text-align: center;">م</th>
                        <th style="padding: 8px; border: 1px solid #333; text-align: center;">كود الصنف</th>
                        <th style="padding: 8px; border: 1px solid #333; text-align: right;">وصف الصنف</th>
                        <th style="padding: 8px; border: 1px solid #333; text-align: center;">الكمية</th>
                        <th style="padding: 8px; border: 1px solid #333; text-align: left;">سعر الوحدة (ج.م)</th>
                        <th style="padding: 8px; border: 1px solid #333; text-align: left;">الإجمالي (ج.م)</th>
                    </tr>
                </thead>
                <tbody>${tableRows}</tbody>
            </table>

            <div style="margin-top: 20px; text-align: left;">
                <table style="width: 300px; margin-right: 0; margin-left: auto; border-collapse: collapse;">
                    ${subtotal > 0 ? `
                    <tr>
                        <td style="padding: 5px; border: none;"><strong>الإجمالي قبل الضريبة:</strong></td>
                        <td style="padding: 5px; border: none; text-align: left;">${formatCurrency(subtotal)} ج.م</td>
                    </tr>` : ''}
                    ${tax > 0 ? `
                    <tr>
                        <td style="padding: 5px; border: none;"><strong>ضريبة القيمة المضافة (14%):</strong></td>
                        <td style="padding: 5px; border: none; text-align: left;">${formatCurrency(tax)} ج.م</td>
                    </tr>` : ''}
                    ${total > 0 ? `
                    <tr style="border-top: 2px solid #198a11;">
                        <td style="padding: 8px 5px; border: none;"><strong>الإجمالي الكلي:</strong></td>
                        <td style="padding: 8px 5px; border: none; text-align: left; color: #198a11; font-size: 1.1em;"><strong>${formatCurrency(total)} ج.م</strong></td>
                    </tr>` : ''}
                </table>
            </div>

            ${total > 0 && totalInWords ? `<div style="margin-top: 10px; font-size: 12px; text-align: left;">فقط ${totalInWords}</div>` : ''}

            ${notes ? `
            <div style="margin-top: 20px;">
                <div class="doc-section-title">ملاحظات:</div>
                <div style="font-size: 11px; white-space: pre-line;">${escapeHtml(notes)}</div>
            </div>` : ''}

            <div style="margin: 20px 0; padding: 15px; border: 1px solid #333; background: #f9f9f9; font-size: 11px;">
                <strong>ملاحظة هامة:</strong> هذا العرض ساري لمدة ${escapeHtml(validity)} ولا يشمل أسعار النقل والشحن.
            </div>

            ${getDocSignatures()}
            ${getDocFooter()}
        </div>
    `;
}

function escapeHtml(str) {
    if (!str) return '';
    if (escapeHtmlCache.has(str)) return escapeHtmlCache.get(str);
    
    const result = str
        .replace(/&/g, '&amp;')
        .replace(/</g, '&lt;')
        .replace(/>/g, '&gt;')
        .replace(/"/g, '&quot;')
        .replace(/'/g, '&#039;');
    
    if (str.length < 100) {
        escapeHtmlCache.set(str, result);
    }
    
    return result;
}

function generateComplaintHTML(complaint) {
    const docNumber = complaint['معرف'] || '';
    const formattedDate = formatDate(complaint['التاريخ'], true);
    const employee = complaint['الموظف'] || '';
    const customer = complaint['العميل'] || '';
    const phone = complaint['رقم_الهاتف'] || '';
    const contactPerson = complaint['مسؤول_التواصل'] || '';
    const contactPhone = complaint['رقم_مسؤول_التواصل'] || '';
    const type = complaint['النوع'] || '';
    const method = complaint['طريقة_الشكوى'] || '';
    const description = complaint['الوصف'] || '';
    
    return `
        <div class="doc-container">
            ${getDocHeader('تقرير شكوى', docNumber, formattedDate, employee)}
            
            <div class="doc-section">
                <div class="doc-section-title">بيانات العميل</div>
                <div class="row">
                    <div class="col-6">
                        <div class="doc-info-row"><span class="doc-info-label">اسم العميل:</span> ${customer || '-'}</div>
                        <div class="doc-info-row"><span class="doc-info-label">رقم الهاتف:</span> ${phone || '-'}</div>
                    </div>
                    <div class="col-6">
                        <div class="doc-info-row"><span class="doc-info-label">مسؤول التواصل:</span> ${contactPerson || '-'}</div>
                        <div class="doc-info-row"><span class="doc-info-label">رقم مسؤول التواصل:</span> ${contactPhone || '-'}</div>
                    </div>
                </div>
            </div>

            <div class="doc-section">
                <div class="doc-section-title">تفاصيل الشكوى</div>
                <div class="row">
                    <div class="col-6">
                        <div class="doc-info-row"><span class="doc-info-label">نوع الشكوى:</span> ${type || '-'}</div>
                    </div>
                    <div class="col-6">
                        <div class="doc-info-row"><span class="doc-info-label">طريقة الاستلام:</span> ${method || '-'}</div>
                    </div>
                </div>
            </div>

            <div class="doc-section">
                <div class="doc-section-title">وصف الشكوى</div>
                <div style="font-size: 12px; line-height: 1.8; white-space: pre-line;">${description || '-'}</div>
            </div>

            <div class="doc-signatures" style="margin-top: 40px;">
                <div class="doc-signature-box">
                    <div class="doc-signature-line"></div>
                    <div class="doc-signature-label">توقيع مقدم الشكوى</div>
                </div>
                <div class="doc-signature-box">
                    <div class="doc-signature-line"></div>
                    <div class="doc-signature-label">توقيع مسؤول خدمة العملاء</div>
                </div>
            </div>

            ${getDocFooter()}
        </div>
    `;
}

function generateCustomerHTML(customer) {
    const docNumber = getSafeValue(customer, 'معرف') || '';
    const formattedDate = formatDate(getSafeValue(customer, 'التاريخ'), true);
    const employee = getSafeValue(customer, 'الموظف') || '';
    const name = getSafeValue(customer, 'اسم_العميل') || '';
    const phone = getSafeValue(customer, 'رقم_الهاتف') || '';
    const email = getSafeValue(customer, 'البريد_الإلكتروني') || '';
    const address = getSafeValue(customer, 'العنوان') || '';
    const notes = getSafeValue(customer, 'الملاحظات') || '';
    const status = getSafeValue(customer, 'الحالة') || 'قيد الاعتماد';
    
    // الحقول الجديدة
    const customerType = getSafeValue(customer, 'نوع_العميل') || '';
    const contactPerson = getSafeValue(customer, 'مسؤول_العميل') || '';
    const contactPhone = getSafeValue(customer, 'هاتف_مسؤول_العميل') || '';
    const taxCard = getSafeValue(customer, 'البطاقة_الضريبية') || '';
    const idCard = getSafeValue(customer, 'البطاقة_الشخصية') || '';
    const passport = getSafeValue(customer, 'الباسبور') || '';
    
    // المرفقات
    const attachments = getSafeValue(customer, 'المرفق') || getSafeValue(customer, 'المرفقات') || '';
    
    let attachmentsHtml = '';
    if (attachments) {
        const files = attachments.split(',').filter(f => f && f.trim());
        if (files.length > 0) {
            attachmentsHtml = `
                <div class="doc-section" style="margin-top: 20px;">
                    <div class="doc-section-title" style="background: #f3f4f6; padding: 10px; border-radius: 8px; margin-bottom: 15px; font-weight: bold;">
                        <i class="ri-attachment-2-line"></i> المرفقات (${files.length})
                    </div>
                    <div class="doc-attachments" style="display: flex; flex-wrap: wrap; gap: 15px; margin-top: 10px;">
                        ${files.map(url => {
                            const trimmedUrl = url.trim();
                            const isImage = /\.(jpg|jpeg|png|gif|webp|bmp|svg)$/i.test(trimmedUrl);
                            const isPdf = /\.pdf$/i.test(trimmedUrl);
                            const fileName = trimmedUrl.split('/').pop() || 'ملف';
                            
                            if (isImage) {
                                // معاينة الصورة بشكل مصغر مع إمكانية التكبير
                                return `
                                    <div class="attachment-preview" style="border: 1px solid #e5e7eb; border-radius: 12px; padding: 8px; background: white; width: 160px; text-align: center; transition: all 0.3s; cursor: pointer;" onclick="showFullImagePreview('${trimmedUrl}')">
                                        <img src="${trimmedUrl}" alt="${fileName}" 
                                             style="width: 140px; height: 140px; object-fit: cover; border-radius: 8px; margin-bottom: 8px; border: 1px solid #e5e7eb; transition: transform 0.2s;">
                                        <div style="font-size: 11px; color: #166534; word-break: break-all; margin-top: 5px;">${fileName.substring(0, 20)}${fileName.length > 20 ? '...' : ''}</div>
                                        <div style="font-size: 10px; color: #888; margin-top: 3px;">اضغط للتكبير</div>
                                    </div>
                                `;
                            } else if (isPdf) {
                                // معاينة PDF باستخدام iframe مصغر
                                return `
                                    <div class="attachment-preview" style="border: 1px solid #e5e7eb; border-radius: 12px; padding: 8px; background: #f9fafb; width: 200px;">
                                        <div style="font-size: 12px; font-weight: bold; margin-bottom: 5px; text-align: center;">📄 ${fileName.substring(0, 20)}</div>
                                        <iframe src="${trimmedUrl}" style="width: 100%; height: 150px; border: none; border-radius: 8px;" frameborder="0"></iframe>
                                        <button onclick="window.open('${trimmedUrl}', '_blank')" style="margin-top: 8px; background: #166534; color: white; border: none; border-radius: 6px; padding: 5px 10px; font-size: 11px; cursor: pointer; width: 100%;">
                                            <i class="ri-external-link-line"></i> فتح PDF
                                        </button>
                                    </div>
                                `;
                            } else {
                                // باقي الملفات (Word, Excel, إلخ)
                                return `
                                    <div class="attachment-preview" style="border: 1px solid #e5e7eb; border-radius: 12px; padding: 8px; background: #f9fafb; width: 160px; text-align: center;">
                                        <div style="width: 140px; height: 140px; background: #f3f4f6; border-radius: 8px; display: flex; align-items: center; justify-content: center; margin-bottom: 8px;">
                                            <i class="ri-file-line" style="font-size: 48px; color: #6b7280;"></i>
                                        </div>
                                        <div style="font-size: 11px; color: #166534; word-break: break-all;">${fileName.substring(0, 20)}${fileName.length > 20 ? '...' : ''}</div>
                                        <button onclick="window.open('${trimmedUrl}', '_blank')" style="margin-top: 8px; background: #166534; color: white; border: none; border-radius: 6px; padding: 4px 8px; font-size: 11px; cursor: pointer;">
                                            <i class="ri-eye-line"></i> معاينة
                                        </button>
                                    </div>
                                `;
                            }
                        }).join('')}
                    </div>
                </div>
            `;
        }
    }
    
    // نوع العميل
    let customerTypeText = '';
    let specialCardHtml = '';
    
    switch(customerType) {
        case 'شركة':
            customerTypeText = '🏢 شركة';
            if (taxCard) {
                specialCardHtml = `<div class="doc-info-row"><span class="doc-info-label">📋 البطاقة الضريبية:</span> ${taxCard}</div>`;
            }
            break;
        case 'شخص':
            customerTypeText = '👤 شخص';
            if (idCard) {
                specialCardHtml = `<div class="doc-info-row"><span class="doc-info-label">🪪 البطاقة الشخصية:</span> ${idCard}</div>`;
            }
            break;
        case 'عميل خارجي':
            customerTypeText = '🌍 عميل خارجي';
            if (passport) {
                specialCardHtml = `<div class="doc-info-row"><span class="doc-info-label"> الباسبور:</span> ${passport}</div>`;
            }
            break;
        default:
            customerTypeText = '❓ غير محدد';
    }
    
    let statusClass = '';
    let statusText = '';
    if (status === 'معتمد') {
        statusClass = 'badge-approved';
        statusText = '✅ معتمد';
    } else if (status === 'مرفوض') {
        statusClass = 'badge-rejected';
        statusText = '❌ مرفوض';
    } else {
        statusClass = 'badge-pending';
        statusText = '⏳ قيد الاعتماد';
    }
    
    return `
        <div class="doc-container" style="font-family: 'Tajawal', sans-serif; max-width: 100%; margin: 0 auto; background: white; border-radius: 16px; overflow: hidden;">
            ${getDocHeader('بيانات عميل', docNumber, formattedDate, employee)}
            
            <div style="margin: 15px 0; text-align: center;">
                <span style="display: inline-block; background: linear-gradient(135deg, #166534, #059669); color: white; padding: 6px 20px; border-radius: 30px; font-size: 14px; font-weight: bold;">
                    ${customerTypeText}
                </span>
            </div>
            
            <div class="doc-section" style="background: #f9fafb; border-radius: 12px; padding: 15px; margin-bottom: 15px;">
                <div class="doc-section-title" style="font-weight: bold; margin-bottom: 10px;"> المعلومات الأساسية</div>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 10px;">
                    <div><strong>️ اسم العميل:</strong> ${escapeHtml(name) || '-'}</div>
                    <div><strong> رقم الهاتف:</strong> ${phone || '-'}</div>
                    <div><strong>✉ البريد الإلكتروني:</strong> ${email || '-'}</div>
                    <div><strong> العنوان:</strong> ${escapeHtml(address) || '-'}</div>
                </div>
            </div>
            
            ${(contactPerson || contactPhone) ? `
            <div class="doc-section" style="background: #f9fafb; border-radius: 12px; padding: 15px; margin-bottom: 15px;">
                <div class="doc-section-title" style="font-weight: bold; margin-bottom: 10px;"> جهة الاتصال المسؤولة</div>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 10px;">
                    <div><strong> مسؤول العميل:</strong> ${escapeHtml(contactPerson) || '-'}</div>
                    <div><strong> هاتف مسؤول العميل:</strong> ${contactPhone || '-'}</div>
                </div>
                ${specialCardHtml}
            </div>
            ` : ''}
            
            ${(!contactPerson && !contactPhone && specialCardHtml) ? `
            <div class="doc-section" style="background: #f9fafb; border-radius: 12px; padding: 15px; margin-bottom: 15px;">
                <div class="doc-section-title" style="font-weight: bold; margin-bottom: 10px;"> بيانات الوثائق</div>
                ${specialCardHtml}
            </div>
            ` : ''}
            
            <div class="doc-section" style="background: #f9fafb; border-radius: 12px; padding: 15px; margin-bottom: 15px;">
                <div style="display: flex; justify-content: space-between; flex-wrap: wrap; gap: 10px;">
                    <div><strong>الحالة:</strong> <span class="badge ${statusClass}">${statusText}</span></div>
                    <div><strong> منشئ المستند:</strong> ${employee || '-'}</div>
                    <div><strong> تاريخ الإنشاء:</strong> ${formattedDate || '-'}</div>
                </div>
            </div>
            
            ${notes ? `
            <div class="doc-notes" style="background: #fffbeb; border-right: 4px solid #f59e0b; border-radius: 8px; padding: 12px; margin-bottom: 15px;">
                <strong> ملاحظات:</strong>
                <div style="margin-top: 5px; white-space: pre-line;">${escapeHtml(notes)}</div>
            </div>
            ` : ''}
            
            ${attachmentsHtml}
            
            ${getDocSignatures()}
            ${getDocFooter()}
        </div>
    `;
}

function generateVisitHTML(visit) {
    const docNumber = visit['معرف'] || '';
    const formattedDate = formatDate(visit['التاريخ'], true);
    const employee = visit['الموظف'] || '';
    const customer = visit['العميل'] || '';
    const location = visit['الموقع'] || '';
    const checkIn = formatTimeOnly(visit['وقت_الدخول']);
    const checkOut = formatTimeOnly(visit['وقت_الخروج']);
    const purpose = visit['الغرض'] || '';
    const result = visit['النتيجة'] || '';
    const notes = visit['الملاحظات'] || '';
    
    return `
        <div class="doc-container">
            ${getDocHeader('تقرير زيارة', docNumber, formattedDate, employee)}
            
            <div class="doc-section">
                <div class="row">
                    <div class="col-6">
                        <div class="doc-info-row"><span class="doc-info-label">العميل:</span> ${customer || '-'}</div>
                        <div class="doc-info-row"><span class="doc-info-label">الموقع:</span> ${location || '-'}</div>
                    </div>
                    <div class="col-6">
                        <div class="doc-info-row"><span class="doc-info-label">وقت الدخول:</span> ${checkIn}</div>
                        <div class="doc-info-row"><span class="doc-info-label">وقت الخروج:</span> ${checkOut}</div>
                    </div>
                </div>
            </div>

            <div class="doc-section">
                <div class="doc-section-title">الغرض من الزيارة</div>
                <div style="font-size: 12px;">${purpose || '-'}</div>
            </div>

            <div class="doc-section">
                <div class="doc-section-title">النتيجة</div>
                <div style="font-size: 12px;">${result || '-'}</div>
            </div>

            ${notes ? `
            <div class="doc-notes">
                <div class="doc-section-title">ملاحظات:</div>
                <div style="font-size: 11px;">${notes}</div>
            </div>` : ''}

            ${getDocSignatures()}
            ${getDocFooter()}
        </div>
    `;
}



function generateActivityHTML(activity) {
    const docNumber = getSafeValue(activity, 'معرف') || '';
    const formattedDate = formatDate(getSafeValue(activity, 'التاريخ'), true);
    const employee = getSafeValue(activity, 'الموظف') || '';
    const notes = getSafeValue(activity, 'ملاحظات') || '';
    
    // محاولة قراءة الإجماليات من عدة مصادر
    let totalSales = 0;
    let totalCollection = 0;
    
    // المصدر 1: الحقول المباشرة
    totalSales = parseFloat(getSafeValue(activity, 'إجمالي_مبيعات_اليوم')) || 0;
    totalCollection = parseFloat(getSafeValue(activity, 'إجمالي_تحصيل_اليوم')) || 0;
    
    let details = [];
    try {
        const detailsRaw = getSafeValue(activity, 'تفاصيل_النشاطات');
        details = typeof detailsRaw === 'string' ? JSON.parse(detailsRaw) : (detailsRaw || []);
        if (!Array.isArray(details)) details = [];
    } catch(e) {
        console.error('خطأ في تحليل تفاصيل النشاط:', e);
        details = [];
    }
    
    // المصدر 2: حساب الإجماليات من التفاصيل إذا كانت الحقول المباشرة صفر
    if (totalSales === 0 && totalCollection === 0 && details.length > 0) {
        details.forEach(d => {
            totalSales += parseFloat(d.salesToday) || 0;
            totalCollection += parseFloat(d.collectionToday) || 0;
        });
    }
    
    console.log('📊 إجمالي المبيعات:', totalSales);
    console.log('📊 إجمالي التحصيل:', totalCollection);
    console.log('📊 عدد التفاصيل:', details.length);
    
    // بناء جدول التفاصيل
    let detailsRows = '';
    if (details.length === 0) {
        detailsRows = '<tr><td colspan="11" class="text-center py-8 text-gray-500">لا توجد تفاصيل للنشاط</td</tr>';
    } else {
        detailsRows = details.map((d, i) => {
            const clientName = d.client || '-';
            const address = d.address || '-';
            const phone = d.phone || '-';
            const subject = d.subject || '-';
            const whatDone = d.whatDone || '-';
            const salesToday = parseFloat(d.salesToday) || 0;
            const collectionToday = parseFloat(d.collectionToday) || 0;
            const fromTime = d.fromTime || '-';
            const toTime = d.toTime || '-';
            
            return `
                <tr class="border-b border-gray-100 hover:bg-gray-50">
                    <td class="px-3 py-2 text-center text-sm">${i + 1}</td>
                    <td class="px-3 py-2 text-sm font-medium">${escapeHtml(clientName)}</td>
                    <td class="px-3 py-2 text-sm">${escapeHtml(address)}</td>
                    <td class="px-3 py-2 text-sm text-left" dir="ltr">${phone}</td>
                    <td class="px-3 py-2 text-sm">${escapeHtml(subject)}</td>
                    <td class="px-3 py-2 text-sm">${escapeHtml(whatDone)}</td>
                    <td class="px-3 py-2 text-sm text-center font-bold text-blue-600">${salesToday.toFixed(2)} ج.م</td>
                    <td class="px-3 py-2 text-sm text-center font-bold text-green-600">${collectionToday.toFixed(2)} ج.م</td>
                    <td class="px-3 py-2 text-sm text-center">${fromTime}</td>
                    <td class="px-3 py-2 text-sm text-center">${toTime}</td>
                </tr>
            `;
        }).join('');
    }
    
    return `
        <div class="doc-container" style="font-family: 'Tajawal', sans-serif; max-width: 100%; margin: 0 auto; background: white; border-radius: 16px; overflow: hidden;">
            <!-- Header -->
            <div class="doc-header" style="display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid #198a11; padding-bottom: 10px; margin-bottom: 20px; flex-wrap: wrap; gap: 10px;">
                <div class="doc-header-right" style="text-align: right;">
                    <div style="display: flex; align-items: center; gap: 10px;">
                        <img src="https://g.top4top.io/p_3708dgdoj1.png" alt="Hyma Plastic" style="height: 50px;">
                        <div>
                            <div style="font-weight: bold; font-size: 16px;">Hyma Plastic</div>
                        </div>
                    </div>
                </div>
                <div class="doc-header-center" style="text-align: center;">
                    <h1 style="margin: 0; font-size: 22px; color: #198a11;">تقرير النشاط اليومي</h1>
                </div>
                <div class="doc-header-left" style="text-align: left; font-size: 12px;">
                    ${docNumber ? `<div><strong>رقم المستند:</strong> ${escapeHtml(docNumber)}</div>` : ''}
                    ${formattedDate ? `<div><strong>التاريخ:</strong> ${escapeHtml(formattedDate)}</div>` : ''}
                    ${employee ? `<div><strong>مسئول المبيعات:</strong> ${escapeHtml(employee)}</div>` : ''}
                </div>
            </div>
            
            <!-- Summary Cards -->
            <div style="display: flex; gap: 20px; margin-bottom: 25px; flex-wrap: wrap;">
                <div style="flex: 1; background: linear-gradient(135deg, #dbeafe, #eff6ff); border-radius: 12px; padding: 15px; text-align: center; border: 1px solid #bfdbfe;">
                    <div style="font-size: 14px; color: #1e40af; margin-bottom: 5px;">💰 إجمالي مبيعات اليوم</div>
                    <div style="font-size: 28px; font-weight: bold; color: #1e40af;">${totalSales.toFixed(2)}</div>
                    <div style="font-size: 12px; color: #1e40af;">جنية مصري</div>
                </div>
                <div style="flex: 1; background: linear-gradient(135deg, #dcfce7, #f0fdf4); border-radius: 12px; padding: 15px; text-align: center; border: 1px solid #bbf7d0;">
                    <div style="font-size: 14px; color: #166534; margin-bottom: 5px;">💵 إجمالي تحصيل اليوم</div>
                    <div style="font-size: 28px; font-weight: bold; color: #166534;">${totalCollection.toFixed(2)}</div>
                    <div style="font-size: 12px; color: #166534;">جنية مصري</div>
                </div>
                <div style="flex: 1; background: linear-gradient(135deg, #fef3c7, #fffbeb); border-radius: 12px; padding: 15px; text-align: center; border: 1px solid #fde68a;">
                    <div style="font-size: 14px; color: #92400e; margin-bottom: 5px;">📊 عدد الأنشطة</div>
                    <div style="font-size: 28px; font-weight: bold; color: #92400e;">${details.length}</div>
                    <div style="font-size: 12px; color: #92400e;">نشاط مسجل</div>
                </div>
            </div>
            
            <!-- Activities Table -->
            <div style="margin-bottom: 20px;">
                <div style="background: #f3f4f6; padding: 10px 15px; border-radius: 8px; margin-bottom: 15px; font-weight: bold;">
                    <i class="ri-list-check-2"></i> تفاصيل الأنشطة
                </div>
                <div style="overflow-x: auto;">
                    <table style="width: 100%; border-collapse: collapse; border: 1px solid #e5e7eb; border-radius: 12px; font-size: 13px;">
                        <thead>
                            <tr style="background: #f9fafb; border-bottom: 2px solid #e5e7eb;">
                                <th style="padding: 12px 8px; text-align: center; width: 3%;">#</th>
                                <th style="padding: 12px 8px; text-align: right; width: 12%;">اسم العميل</th>
                                <th style="padding: 12px 8px; text-align: right; width: 10%;">العنوان</th>
                                <th style="padding: 12px 8px; text-align: center; width: 8%;">الهاتف</th>
                                <th style="padding: 12px 8px; text-align: right; width: 12%;">الموضوع</th>
                                <th style="padding: 12px 8px; text-align: right; width: 12%;">ما تم</th>
                                <th style="padding: 12px 8px; text-align: center; width: 8%;">مبيعات اليوم</th>
                                <th style="padding: 12px 8px; text-align: center; width: 8%;">تحصيل اليوم</th>
                                <th style="padding: 12px 8px; text-align: center; width: 6%;">من وقت</th>
                                <th style="padding: 12px 8px; text-align: center; width: 6%;">إلى وقت</th>
                            </tr>
                        </thead>
                        <tbody>
                            ${detailsRows}
                        </tbody>
                    </table>
                </div>
            </div>
            
            <!-- Notes -->
            ${notes ? `
            <div style="background: #fffbeb; border-right: 4px solid #f59e0b; border-radius: 8px; padding: 15px; margin-bottom: 20px;">
                <div style="font-weight: bold; margin-bottom: 8px;">
                    <i class="ri-sticky-note-line"></i> ملاحظات عامة:
                </div>
                <div style="font-size: 13px; line-height: 1.6; white-space: pre-line;">${escapeHtml(notes)}</div>
            </div>
            ` : ''}
            
            <!-- Footer -->
            <div style="border-top: 2px solid #198a11; margin-top: 20px; padding-top: 15px; text-align: center; font-size: 11px; color: #666;">
                <div>www.Hyma-Plastic.com</div>
                <div>sales@hyma-plastic.com | export@hyma-plastic.com | office@hyma-plastic.com</div>
                <div>العنوان: 22 حدائق العبور - ش صالح سالم - مدينة نصر - القاهرة - مصر 11811 | ص.ب 8007 مدينة نصر</div>
                <div>ت: 24011626 | فاكس: 24011627</div>
                <div>مصنع: المنصورية، امبابة، جيزة | ت: 38900726 - 38900728</div>
            </div>
        </div>
    `;
}

function generatePlanHTML(plan) {
    const docNumber = plan['معرف'] || '';
    const employee = plan['الموظف'] || '';
    const fromDate = formatDate(plan['من_تاريخ'] || plan['من تاريخ'], true);
    const toDate = formatDate(plan['إلى_تاريخ'] || plan['إلى تاريخ'], true);
    const goals = plan['الأهداف'] || '';
    const tasks = plan['المهام'] || '';
    const notes = plan['الملاحظات'] || '';
    
    return `
        <div class="doc-container">
            ${getDocHeader('الخطة الأسبوعية', docNumber, '', employee)}
            
            <div class="doc-section">
                <div class="row">
                    <div class="col-6">
                        <div class="doc-info-row"><span class="doc-info-label">من تاريخ:</span> ${fromDate || '-'}</div>
                    </div>
                    <div class="col-6">
                        <div class="doc-info-row"><span class="doc-info-label">إلى تاريخ:</span> ${toDate || '-'}</div>
                    </div>
                </div>
            </div>

            <div class="doc-section">
                <div class="doc-section-title">الأهداف</div>
                <div style="font-size: 12px; white-space: pre-line;">${goals || '-'}</div>
            </div>

            <div class="doc-section">
                <div class="doc-section-title">المهام</div>
                <div style="font-size: 12px; white-space: pre-line;">${tasks || '-'}</div>
            </div>

            ${notes ? `
            <div class="doc-notes">
                <div class="doc-section-title">ملاحظات:</div>
                <div style="font-size: 11px;">${notes}</div>
            </div>` : ''}

            ${getDocSignatures()}
            ${getDocFooter()}
        </div>
    `;
}

function generateCollectionHTML(collection) {
    const docNumber = collection['معرف'] || '';
    const formattedDate = formatDate(collection['التاريخ'], true);
    const employee = collection['الموظف'] || '';
    const customer = collection['العميل'] || '';
    const amount = collection['المبلغ_المستحق'] || '';
    const dueDate = formatDate(collection['تاريخ_الاستحقاق'], true);
    const status = collection['الحالة'] || '';
    const notes = collection['الملاحظات'] || '';
    
    return `
        <div class="doc-container">
            ${getDocHeader('تقرير التحصيل', docNumber, formattedDate, employee)}
            
            <div class="doc-section">
                <div class="row">
                    <div class="col-6">
                        <div class="doc-info-row"><span class="doc-info-label">العميل:</span> ${customer || '-'}</div>
                        <div class="doc-info-row"><span class="doc-info-label">المبلغ المستحق:</span> ${amount || '-'} جنيه</div>
                    </div>
                    <div class="col-6">
                        <div class="doc-info-row"><span class="doc-info-label">تاريخ الاستحقاق:</span> ${dueDate || '-'}</div>
                        <div class="doc-info-row"><span class="doc-info-label">الحالة:</span> ${status || '-'}</div>
                    </div>
                </div>
            </div>

            ${notes ? `
            <div class="doc-notes">
                <div class="doc-section-title">ملاحظات:</div>
                <div style="font-size: 11px;">${notes}</div>
            </div>` : ''}

            ${getDocSignatures()}
            ${getDocFooter()}
        </div>
    `;
}

function showDocumentPreview(item, type) {
    let html = '';
    const status = getSafeValue(item, 'الحالة');
    
    console.log('Preview item:', item);
    
    switch(type) {
        case 'sale':
            html = generateSalesOrderHTML(item);
            break;
        case 'quote':
            html = generateQuoteHTML(item);
            break;
        case 'complaint':
            html = generateComplaintHTML(item);
            break;
        case 'customer':
            html = generateCustomerHTML(item);
            break;
        case 'visit':
            html = generateVisitHTML(item);
            break;
        case 'activity':
            html = generateActivityHTML(item);
            break;
        case 'plan':
            html = generatePlanHTML(item);
            break;
        case 'collection':
            html = generateCollectionHTML(item);
            break;
        default:
            html = '<div style="padding: 40px; text-align: center;">نوع المستند غير معروف</div>';
    }
    
    const titles = {
        sale: 'أمر بيع', quote: 'عرض سعر', complaint: 'شكوى', 
        customer: 'بيانات عميل', visit: 'زيارة', activity: 'نشاط يومي', 
        plan: 'خطة أسبوعية', collection: 'تحصيل'
    };
    
    const titleEl = document.getElementById('preview-modal-title');
    if (titleEl) {
        titleEl.innerHTML = `<i class="ri-file-text-line text-primary ml-2"></i> عرض ${titles[type] || 'مستند'}`;
    }
    
    const contentDiv = document.getElementById('preview-content');
    if (contentDiv) {
        contentDiv.innerHTML = html;
        
        if (status === 'قيد الاعتماد') {
            contentDiv.classList.add('watermark');
        } else {
            contentDiv.classList.remove('watermark');
        }
    }
    
    const modal = document.getElementById('preview-modal');
    if (modal) modal.classList.remove('hidden');
}

// ═══════════════════════════════════════════════════════════════════════════
// القسم الرابع: دوال عرض الواجهات والتنقل (محسنة)
// ═══════════════════════════════════════════════════════════════════════════

function showPage(pageId) {
    document.querySelectorAll('[id$="-page"]').forEach(el => {
        el.classList.add('hidden');
    });
    
    const targetPage = document.getElementById(pageId);
    if (targetPage) {
        targetPage.classList.remove('hidden');
        targetPage.scrollTop = 0;
    }
    
    if (pageId !== 'login-page' && Date.now() - appCache.timestamp > appCache.CACHE_DURATION) {
        loadUserData();
    }
    
    if (['add-sales-page', 'add-quote-page', 'add-complaint-page', 'add-visit-page', 'add-collection-page', 'add-activity-page'].includes(pageId)) {
        dropdownsInitialized = false;
        requestAnimationFrame(() => initSearchableDropdowns());
    }
    
    if (pageId === 'add-activity-page') {
        const dateField = document.getElementById('activity-date');
        const today = new Date().toISOString().split('T')[0];
        if (dateField) dateField.value = today;
        
        const tbody = document.getElementById('activities-detail-body');
        if (tbody && tbody.children.length === 0) {
            addActivityRow();
        }
    }
}

function loadUserData() {
    if (!currentUser) return;
    
    const userData = {
        'user-name': currentUser.username,
        'user-role': currentUser.role === 'admin' ? 'مسؤول' : currentUser.role === 'manager' ? 'مدير' : 'موظف',
        'customer-page-username': currentUser.username,
        'customer-page-role': currentUser.role,
        'add-customer-username': currentUser.username,
        'add-customer-role': currentUser.role,
        'plan-page-username': currentUser.username,
        'plan-page-role': currentUser.role,
        'add-plan-username': currentUser.username,
        'add-plan-role': currentUser.role,
        'visit-page-username': currentUser.username,
        'visit-page-role': currentUser.role,
        'add-visit-username': currentUser.username,
        'add-visit-role': currentUser.role,
        'activity-page-username': currentUser.username,
        'activity-page-role': currentUser.role,
        'add-activity-username': currentUser.username,
        'add-activity-role': currentUser.role,
        'quote-page-username': currentUser.username,
        'quote-page-role': currentUser.role,
        'add-quote-username': currentUser.username,
        'add-quote-role': currentUser.role,
        'sale-page-username': currentUser.username,
        'sale-page-role': currentUser.role,
        'add-sale-username': currentUser.username,
        'add-sale-role': currentUser.role,
        'complaint-page-username': currentUser.username,
        'complaint-page-role': currentUser.role,
        'add-complaint-username': currentUser.username,
        'add-complaint-role': currentUser.role,
        'collection-page-username': currentUser.username,
        'collection-page-role': currentUser.role,
        'add-collection-username': currentUser.username,
        'add-collection-role': currentUser.role,
        'profile-user-name': currentUser.username,
        'profile-user-role': currentUser.role,
        'profile-username': currentUser.username,
        'profile-email': currentUser.email || ''
    };
    
    Object.entries(userData).forEach(([id, value]) => {
        const el = document.getElementById(id);
        if (el) {
            if (el.tagName === 'INPUT') {
                el.value = value;
            } else {
                el.textContent = value;
            }
        }
    });
}

// ═══════════════════════════════════════════════════════════════════════════
// القسم الخامس: دوال الحفظ (محسنة لمنع التكرار والتداخل)
// ═══════════════════════════════════════════════════════════════════════════

function getActivityRowsData() {
    const rows = document.querySelectorAll('#activities-detail-body tr');
    const data = [];
    
    rows.forEach(row => {
        const clientSelect = row.querySelector('.activity-client');
        let client = '';
        if (clientSelect) {
            const selectedOption = clientSelect.options[clientSelect.selectedIndex];
            client = selectedOption ? selectedOption.text : '';
        }
        
        const address = row.querySelector('.activity-address')?.value || '';
        const phone = row.querySelector('.activity-phone')?.value || '';
        const subject = row.querySelector('.activity-subject')?.value || '';
        const whatDone = row.querySelector('.activity-what-done')?.value || '';
        const salesToday = parseFloat(row.querySelector('.activity-sales')?.value) || 0;
        const collectionToday = parseFloat(row.querySelector('.activity-collection')?.value) || 0;
        const fromTime = row.querySelector('.activity-from-time')?.value || '';
        const toTime = row.querySelector('.activity-to-time')?.value || '';
        
        // إضافة الصف فقط إذا كان يحتوي على بيانات مفيدة
        if (client || subject || whatDone || salesToday > 0 || collectionToday > 0) {
            data.push({
                client: client,
                address: address,
                phone: phone,
                subject: subject,
                whatDone: whatDone,
                salesToday: salesToday,
                collectionToday: collectionToday,
                fromTime: fromTime,
                toTime: toTime
            });
        }
    });
    
    return data;
}

function getQuoteItemsData() {
    const rows = document.querySelectorAll('#quote-items-body tr');
    const data = [];
    rows.forEach(row => {
        const code = row.querySelector('.quote-item-code')?.value || '';
        const name = row.querySelector('.quote-item-name')?.value || '';
        const qty = row.querySelector('.quote-qty')?.value || '';
        const unit = row.querySelector('.quote-unit')?.value || '';
        if (code || name || qty) {
            data.push({ code, name, qty, unit });
        }
    });
    return data;
}

function getSaleItemsData() {
    const rows = document.querySelectorAll('#sale-items-body tr');
    const data = [];
    rows.forEach(row => {
        const code = row.querySelector('.sale-item-code')?.value || '';
        const name = row.querySelector('.sale-item-name')?.value || '';
        const qty = row.querySelector('.sale-qty')?.value || '';
        const unit = row.querySelector('.sale-unit')?.value || '';
        const unitPrice = row.querySelector('.sale-unit-price')?.value || '';
        const discount = row.querySelector('.sale-discount')?.value || '0';
        const total = row.querySelector('.sale-item-total')?.value || '';
        if (code || name || qty || unit || unitPrice) 
            data.push({ code, name, qty, unit, unitPrice, discount, total });
    });
    return data;
}

async function getExistingCustomerStatus(id) {
    if (!appCache.data.customers) return 'قيد الاعتماد';
    const strId = String(id);
    const existing = appCache.data.customers.find(c => String(getSafeValue(c, 'معرف')) === strId);
    return existing ? (getSafeValue(existing, 'الحالة') || 'قيد الاعتماد') : 'قيد الاعتماد';
}

async function getExistingQuoteStatus(id) {
    if (!appCache.data.quotes) return 'قيد الاعتماد';
    const strId = String(id);
    const existing = appCache.data.quotes.find(q => String(getSafeValue(q, 'معرف')) === strId);
    return existing ? (getSafeValue(existing, 'الحالة') || 'قيد الاعتماد') : 'قيد الاعتماد';
}

async function getExistingSaleStatus(id) {
    if (!appCache.data.sales) return 'قيد الاعتماد';
    const strId = String(id);
    const existing = appCache.data.sales.find(s => String(getSafeValue(s, 'معرف')) === strId);
    return existing ? (getSafeValue(existing, 'الحالة') || 'قيد الاعتماد') : 'قيد الاعتماد';
}

// ==============================================
// دوال التحكم في حقول البطاقات حسب نوع العميل
// ==============================================

function toggleCustomerCardFields() {
    const customerType = document.getElementById('customer-type')?.value;
    
    const taxCardField = document.getElementById('tax-card-field');
    const idCardField = document.getElementById('id-card-field');
    const passportField = document.getElementById('passport-field');
    
    // إخفاء الكل أولاً
    if (taxCardField) taxCardField.style.display = 'none';
    if (idCardField) idCardField.style.display = 'none';
    if (passportField) passportField.style.display = 'none';
    
    // إظهار الحقل المناسب حسب نوع العميل
    if (customerType === 'شركة') {
        if (taxCardField) taxCardField.style.display = 'block';
    } else if (customerType === 'شخص') {
        if (idCardField) idCardField.style.display = 'block';
    } else if (customerType === 'عميل خارجي') {
        if (passportField) passportField.style.display = 'block';
    }
}

// ==============================================
// تحديث دالة saveCustomer لتشمل الحقول الجديدة
// ==============================================

// استبدل دالة saveCustomer الموجودة بهذه النسخة المحدثة
async function saveCustomer(e) {
    e.preventDefault();
    
    const id = document.getElementById('customer-id')?.value;
    const cacheKey = `customer-${id || 'new'}`;
    
    if (pendingSaves.has(cacheKey)) return;
    pendingSaves.set(cacheKey, true);
    
    if (isSavingCustomer) return;
    isSavingCustomer = true;

    const btn = document.getElementById('save-customer-btn');
    const originalText = btn?.innerHTML;
    if (btn) {
        btn.innerHTML = '<i class="ri-loader-4-line animate-spin"></i> جاري حفظ العميل...';
        btn.disabled = true;
    }

    try {
        const name = document.getElementById('customer-name')?.value.trim();
        if (!name) { 
            showError('اسم العميل مطلوب'); 
            return; 
        }

        const customerType = document.getElementById('customer-type')?.value;
        if (!customerType) {
            showError('يرجى اختيار نوع العميل');
            return;
        }

        let finalId = id || await generateSequentialId('CUS', SHEET_CONFIG.CUSTOMERS_SHEET_NAME);

        const phone = document.getElementById('customer-phone')?.value.trim() || '';
        const email = document.getElementById('customer-email')?.value.trim() || '';
        const address = document.getElementById('customer-address')?.value.trim() || '';
        const notes = document.getElementById('customer-notes')?.value.trim() || '';
        const contactPerson = document.getElementById('customer-contact-person')?.value.trim() || '';
        const contactPhone = document.getElementById('customer-contact-phone')?.value.trim() || '';
        
        // الحقول الخاصة حسب نوع العميل
        let taxCard = '';
        let idCard = '';
        let passport = '';
        
        if (customerType === 'شركة') {
            taxCard = document.getElementById('customer-tax-card')?.value.trim() || '';
        } else if (customerType === 'شخص') {
            idCard = document.getElementById('customer-id-card')?.value.trim() || '';
        } else if (customerType === 'عميل خارجي') {
            passport = document.getElementById('customer-passport')?.value.trim() || '';
        }
        
        const attachments = document.getElementById('customer-attachments');
        let attachmentUrls = [];
        
        if (attachments?.files?.length > 0) {
            const uploadPromises = Array.from(attachments.files).map(async (file) => {
                const base64 = await new Promise((resolve) => {
                    const reader = new FileReader();
                    reader.onload = () => resolve(reader.result.split(',')[1]);
                    reader.readAsDataURL(file);
                });
                const uploadRes = await sendRequest({
                    action: 'UPLOAD_FILE',
                    attachment: base64,
                    filename: file.name,
                    mimeType: file.type
                });
                return (uploadRes.success && (uploadRes.data?.url || uploadRes.url)) ? (uploadRes.data?.url || uploadRes.url) : null;
            });
            
            attachmentUrls = (await Promise.all(uploadPromises)).filter(url => url);
        }

        let finalStatus = id ? (originalCustomerStatus || await getExistingCustomerStatus(id)) : 'قيد الاعتماد';

        const customerData = {
            'معرف': finalId,
            'التاريخ': getCurrentDateTime(),
            'الموظف': currentUser.username,
            'اسم_العميل': name,
            'نوع_العميل': customerType,
            'رقم_الهاتف': phone,
            'البريد_الإلكتروني': email,
            'العنوان': address,
            'ملاحظات': notes,
            'مسؤول_العميل': contactPerson,
            'هاتف_مسؤول_العميل': contactPhone,
            'البطاقة_الضريبية': taxCard,
            'البطاقة_الشخصية': idCard,
            'الباسبور': passport,
            'المرفق': attachmentUrls.join(','),
            'الحالة': finalStatus
        };

        const res = await sendRequest({
            action: id ? 'UPDATE' : 'ADD',
            sheetName: SHEET_CONFIG.CUSTOMERS_SHEET_NAME,
            data: JSON.stringify(customerData),
            id: id
        });
        
        if (res.success) {
            showSuccess(id ? 'تم تحديث العميل' : 'تم إضافة العميل');
            await loadAllData(true);
            showPage('new-customer-page');
            document.getElementById('customer-form')?.reset();
            if (document.getElementById('customer-id')) {
                document.getElementById('customer-id').value = '';
            }
            isEditingCustomer = false;
            editingCustomerId = null;
            originalCustomerStatus = '';
        } else {
            showError(res.error || 'فشل الحفظ');
        }
    } catch (err) {
        showError('خطأ في الاتصال: ' + err.message);
    } finally {
        if (btn) {
            btn.innerHTML = originalText;
            btn.disabled = false;
        }
        isSavingCustomer = false;
        pendingSaves.delete(cacheKey);
    }
}

// ==============================================
// تحديث دالة editCustomer لتشمل الحقول الجديدة
// ==============================================

function editCustomer(id) {
    const customer = appCache.data.customers.find(c => getSafeValue(c, 'معرف') == id);
    if (!customer) return;
    
    const status = getSafeValue(customer, 'الحالة');
    if (status === 'معتمد') {
        showError('لا يمكن تعديل عميل معتمد');
        return;
    }
    
    originalCustomerStatus = status;
    
    isEditingCustomer = true;
    editingCustomerId = id;
    
    const idField = document.getElementById('customer-id');
    const nameField = document.getElementById('customer-name');
    const typeField = document.getElementById('customer-type');
    const phoneField = document.getElementById('customer-phone');
    const emailField = document.getElementById('customer-email');
    const addressField = document.getElementById('customer-address');
    const notesField = document.getElementById('customer-notes');
    const contactPersonField = document.getElementById('customer-contact-person');
    const contactPhoneField = document.getElementById('customer-contact-phone');
    const taxCardField = document.getElementById('customer-tax-card');
    const idCardField = document.getElementById('customer-id-card');
    const passportField = document.getElementById('customer-passport');
    
    if (idField) idField.value = id;
    if (nameField) nameField.value = getSafeValue(customer, 'اسم_العميل') || getSafeValue(customer, 'اسم العميل');
    if (typeField) typeField.value = getSafeValue(customer, 'نوع_العميل') || '';
    if (phoneField) phoneField.value = getSafeValue(customer, 'رقم_الهاتف');
    if (emailField) emailField.value = getSafeValue(customer, 'البريد_الإلكتروني');
    if (addressField) addressField.value = getSafeValue(customer, 'العنوان');
    if (notesField) notesField.value = getSafeValue(customer, 'الملاحظات');
    if (contactPersonField) contactPersonField.value = getSafeValue(customer, 'مسؤول_العميل');
    if (contactPhoneField) contactPhoneField.value = getSafeValue(customer, 'هاتف_مسؤول_العميل');
    if (taxCardField) taxCardField.value = getSafeValue(customer, 'البطاقة_الضريبية');
    if (idCardField) idCardField.value = getSafeValue(customer, 'البطاقة_الشخصية');
    if (passportField) passportField.value = getSafeValue(customer, 'الباسبور');
    
    // إظهار الحقل المناسب حسب نوع العميل
    toggleCustomerCardFields();
    
    showPage('add-customer-page');
}

// ==============================================
// ربط حدث تغيير نوع العميل
// ==============================================

document.getElementById('customer-type')?.addEventListener('change', toggleCustomerCardFields);

async function savePlan(e) {
    e.preventDefault();
    if (isSavingPlan) return;
    isSavingPlan = true;

    const btn = document.getElementById('save-plan-btn');
    const originalText = btn?.innerHTML;
    if (btn) {
        btn.innerHTML = '<i class="ri-loader-4-line animate-spin"></i> جاري حفظ الخطة...';
        btn.disabled = true;
    }

    try {
        const fromDate = document.getElementById('plan-from')?.value;
        const toDate = document.getElementById('plan-to')?.value;
        if (!fromDate || !toDate) { 
            showError('يرجى تحديد الفترة'); 
            return; 
        }

        const planData = {
            'معرف': await generateSequentialId('PLN', SHEET_CONFIG.PLANS_SHEET_NAME),
            'من_تاريخ': fromDate,
            'إلى_تاريخ': toDate,
            'الأهداف': document.getElementById('plan-goals')?.value.trim() || '',
            'المهام': document.getElementById('plan-tasks')?.value.trim() || '',
            'ملاحظات': document.getElementById('plan-notes')?.value.trim() || '',
            'الموظف': currentUser.username,
            'التاريخ': getCurrentDateTime()
        };

        const res = await sendRequest({
            action: 'ADD',
            sheetName: SHEET_CONFIG.PLANS_SHEET_NAME,
            data: JSON.stringify(planData)
        });
        
        if (res.success) {
            showSuccess('تم حفظ الخطة');
            await loadAllData();
            showPage('weekly-plan-page');
            document.getElementById('plan-form')?.reset();
        } else {
            showError(res.error || 'فشل الحفظ');
        }
    } catch (err) {
        showError('خطأ في الاتصال: ' + err.message);
    } finally {
        if (btn) {
            btn.innerHTML = originalText;
            btn.disabled = false;
        }
        isSavingPlan = false;
    }
}

async function saveVisit(e) {
    e.preventDefault();
    if (isSavingVisit) return;
    isSavingVisit = true;

    const btn = document.getElementById('save-visit-btn');
    const originalText = btn?.innerHTML;
    if (btn) {
        btn.innerHTML = '<i class="ri-loader-4-line animate-spin"></i> جاري حفظ الزيارة...';
        btn.disabled = true;
    }

    try {
        const date = document.getElementById('visit-date')?.value;
        const clientSelect = document.getElementById('visit-client-select');
        
        let clientName = '';
        const wrapper = clientSelect?.parentElement?.querySelector('.searchable-wrapper');
        if (wrapper) {
            const searchInput = wrapper.querySelector('input');
            if (searchInput && searchInput.value.trim()) {
                clientName = searchInput.value.trim();
            }
        }
        if (!clientName && clientSelect && clientSelect.selectedIndex !== -1) {
            clientName = clientSelect.options[clientSelect.selectedIndex].text;
        }
        
        if (!date || !clientName) {
            showError('التاريخ والعميل مطلوبان');
            return;
        }

        const newId = await generateSequentialId('VIS', SHEET_CONFIG.VISITS_SHEET_NAME);

        const visitData = {
            'معرف': newId,
            'التاريخ': date,
            'العميل': clientName,
            'الموقع': document.getElementById('visit-location')?.value.trim() || '',
            'وقت_الدخول': document.getElementById('visit-checkin')?.value || '',
            'وقت_الخروج': document.getElementById('visit-checkout')?.value || '',
            'الغرض': document.getElementById('visit-purpose')?.value || '',
            'النتيجة': document.getElementById('visit-result')?.value.trim() || '',
            'ملاحظات': document.getElementById('visit-notes')?.value.trim() || '',
            'الموظف': currentUser.username
        };

        const res = await sendRequest({
            action: 'ADD',
            sheetName: SHEET_CONFIG.VISITS_SHEET_NAME,
            data: JSON.stringify(visitData)
        });
        
        if (res.success) {
            showSuccess('تم حفظ الزيارة');
            await loadAllData(true);
            showPage('visit-report-page');
            document.getElementById('visit-form')?.reset();
            const locField = document.getElementById('visit-location');
            if (locField) locField.value = '';
        } else {
            showError(res.error || 'فشل الحفظ');
        }
    } catch (err) {
        showError('خطأ في الاتصال: ' + err.message);
    } finally {
        if (btn) {
            btn.innerHTML = originalText;
            btn.disabled = false;
        }
        isSavingVisit = false;
    }
}

async function saveActivity(e) {
    e.preventDefault();
    if (isSavingActivity) return;
    isSavingActivity = true;

    const btn = document.getElementById('save-activity-btn');
    const originalText = btn?.innerHTML;
    if (btn) {
        btn.innerHTML = '<i class="ri-loader-4-line animate-spin"></i> جاري حفظ النشاط...';
        btn.disabled = true;
    }

    try {
        const date = document.getElementById('activity-date')?.value;
        if (!date) { 
            showError('التاريخ مطلوب'); 
            return; 
        }

        const details = getActivityRowsData();
        if (details.length === 0) { 
            showError('أضف تفاصيل نشاط واحد على الأقل'); 
            return; 
        }

        // حساب إجمالي المبيعات والتحصيل لليوم
        let totalSalesToday = 0;
        let totalCollectionToday = 0;
        details.forEach(d => {
            totalSalesToday += d.salesToday || 0;
            totalCollectionToday += d.collectionToday || 0;
        });

        const activityData = {
            'معرف': await generateSequentialId('ACT', SHEET_CONFIG.ACTIVITIES_SHEET_NAME),
            'التاريخ': date,
            'تفاصيل_النشاطات': JSON.stringify(details),
            'ملاحظات': document.getElementById('activity-notes')?.value.trim() || '',
            'الموظف': currentUser.username,
            'إجمالي_مبيعات_اليوم': totalSalesToday,
            'إجمالي_تحصيل_اليوم': totalCollectionToday
        };

        const res = await sendRequest({
            action: 'ADD',
            sheetName: SHEET_CONFIG.ACTIVITIES_SHEET_NAME,
            data: JSON.stringify(activityData)
        });
        
        if (res.success) {
            showSuccess('تم حفظ النشاط');
            await loadAllData(true);
            showPage('daily-activity-page');
            
            // إعادة تعيين النموذج
            const activityForm = document.getElementById('activity-form');
            if (activityForm) activityForm.reset();
            
            const tbody = document.getElementById('activities-detail-body');
            if (tbody) tbody.innerHTML = '';
            addActivityRow(); // إضافة صف فارغ جديد
            
            // إعادة تعيين التاريخ والموظف
            const dateField = document.getElementById('activity-date');
            if (dateField) dateField.value = new Date().toISOString().split('T')[0];
            
            const employeeField = document.getElementById('activity-employee');
            if (employeeField && currentUser) employeeField.value = currentUser.username;
        } else {
            showError(res.error || 'فشل الحفظ');
        }
    } catch (err) {
        console.error('خطأ في حفظ النشاط:', err);
        showError('خطأ في الاتصال: ' + err.message);
    } finally {
        if (btn) {
            btn.innerHTML = originalText;
            btn.disabled = false;
        }
        isSavingActivity = false;
    }
}

async function saveQuote(e) {
    e.preventDefault();
    if (isSavingQuote) return;
    isSavingQuote = true;

    const btn = document.getElementById('save-quote-btn');
    const originalText = btn?.innerHTML;
    if (btn) {
        btn.innerHTML = '<i class="ri-loader-4-line animate-spin"></i> جاري حفظ عرض السعر...';
        btn.disabled = true;
    }

    try {
        const date = document.getElementById('quote-date')?.value;
        if (!date) {
            showError('يرجى اختيار التاريخ');
            return;
        }

        const clientSelect = document.getElementById('quote-client-select');
        let clientName = '';
        const wrapper = clientSelect?.parentElement?.querySelector('.searchable-wrapper');
        if (wrapper) {
            const searchInput = wrapper.querySelector('input[type="text"]');
            if (searchInput && searchInput.value.trim()) {
                clientName = searchInput.value.trim();
            }
        }
        if (!clientName && clientSelect && clientSelect.selectedIndex !== -1) {
            clientName = clientSelect.options[clientSelect.selectedIndex].text;
        }

        if (!clientName) {
            showError('يرجى اختيار عميل');
            return;
        }

        const items = getQuoteItemsData();
        if (items.length === 0 || items.every(i => !i.code && !i.name && !i.qty)) {
            showError('أضف صنف واحد على الأقل');
            return;
        }

        const taxType = document.querySelector('input[name="taxTypeQuote"]:checked')?.value || 'exclusive';
        const subtotal = parseFloat(document.getElementById('quote-subtotal-before-tax')?.innerText) || 0;
        const tax = parseFloat(document.getElementById('quote-total-tax')?.innerText) || 0;
        const total = parseFloat(document.getElementById('quote-total-amount')?.innerText) || 0;
        const validity = document.getElementById('quote-validity')?.value || '30 يوم';

        const quoteId = editingQuoteId ? editingQuoteId : await generateSequentialId('QUT', SHEET_CONFIG.QUOTES_SHEET_NAME);

        const quoteData = {
            'معرف': quoteId,
            'التاريخ': date,
            'العميل': clientName,
            'تفاصيل_الأصناف': JSON.stringify(items),
            'طريقة_السداد': document.getElementById('quote-payment-method')?.value.trim() || '',
            'مكان_التسليم': document.getElementById('quote-delivery-place')?.value || '',
            'ملاحظات': document.getElementById('quote-notes')?.value.trim() || '',
            'الموظف': currentUser.username,
            'الحالة': editingQuoteId ? (await getExistingQuoteStatus(editingQuoteId)) : 'قيد الاعتماد',
            'مدة_العرض': validity,
            'نوع_الضريبة': taxType,
            'الإجمالي_قبل_الضريبة': subtotal,
            'الضريبة': tax,
            'الإجمالي_الكلي': total
        };

        const action = editingQuoteId ? 'UPDATE' : 'ADD';
        const res = await sendRequest({
            action: action,
            sheetName: SHEET_CONFIG.QUOTES_SHEET_NAME,
            data: JSON.stringify(quoteData),
            id: editingQuoteId
        });
        
        if (res.success) {
            showSuccess(editingQuoteId ? 'تم تحديث عرض السعر' : 'تم حفظ عرض السعر');
            await loadAllData();
            showPage('quote-page');
            document.getElementById('quote-form')?.reset();
            const itemsBody = document.getElementById('quote-items-body');
            if (itemsBody) itemsBody.innerHTML = '';
            addQuoteItemRow();
            editingQuoteId = null;
            isEditingQuote = false;
        } else {
            showError(res.error || 'فشل الحفظ');
        }
    } catch (err) {
        console.error('خطأ في حفظ عرض السعر:', err);
        showError('خطأ في الاتصال: ' + err.message);
    } finally {
        if (btn) {
            btn.innerHTML = originalText;
            btn.disabled = false;
        }
        isSavingQuote = false;
    }
}

async function saveSale(e) {
    e.preventDefault();
    if (isSavingSale) return;
    isSavingSale = true;

    const btn = document.getElementById('save-sale-btn');
    const originalText = btn?.innerHTML;
    if (btn) {
        btn.innerHTML = '<i class="ri-loader-4-line animate-spin"></i> جاري حفظ أمر البيع...';
        btn.disabled = true;
    }

    try {
        const date = document.getElementById('sale-date')?.value;
        if (!date) {
            showError('يرجى اختيار التاريخ');
            return;
        }

        const clientSelect = document.getElementById('sale-client-select');
        let clientName = '';
        const wrapper = clientSelect?.parentElement?.querySelector('.searchable-wrapper');
        if (wrapper) {
            const searchInput = wrapper.querySelector('input[type="text"]');
            if (searchInput && searchInput.value.trim()) {
                clientName = searchInput.value.trim();
            }
        }
        if (!clientName && clientSelect && clientSelect.selectedIndex !== -1) {
            clientName = clientSelect.options[clientSelect.selectedIndex].text;
        }

        if (!clientName) {
            showError('يرجى اختيار عميل');
            return;
        }

        const items = getSaleItemsData();
        if (items.length === 0 || items.every(i => !i.code && !i.name && !i.qty && !i.unitPrice)) {
            showError('أضف صنف واحد على الأقل');
            return;
        }

        const subtotal = parseFloat(document.getElementById('subtotal-before-tax')?.innerText) || 0;
        const tax = parseFloat(document.getElementById('sale-total-tax')?.innerText) || 0;
        const total = parseFloat(document.getElementById('sale-total-amount')?.innerText) || 0;

        const saleId = editingSaleId ? editingSaleId : await generateSequentialId('SAL', SHEET_CONFIG.SALES_SHEET_NAME);

        const saleData = {
            'معرف': saleId,
            'التاريخ': date,
            'العميل': clientName,
            'تفاصيل_الأصناف': JSON.stringify(items),
            'مكان_التصنيع': document.getElementById('sale-manufacturing-location')?.value || '',
            'طريقة_السداد': document.getElementById('sale-payment-method')?.value.trim() || '',
            'مكان_التسليم': document.getElementById('sale-delivery-place')?.value || '',
            'الشروط_والأحكام': document.getElementById('terms-conditions')?.value.trim() || '',
            'ملاحظات': document.getElementById('sale-notes')?.value.trim() || '',
            'الإجمالي_قبل_الضريبة': subtotal,
            'الضريبة': tax,
            'الإجمالي_الكلي': total,
            'الموظف': currentUser.username,
            'الحالة': editingSaleId ? (await getExistingSaleStatus(editingSaleId)) : 'قيد الاعتماد'
        };

        const action = editingSaleId ? 'UPDATE' : 'ADD';
        const res = await sendRequest({
            action: action,
            sheetName: SHEET_CONFIG.SALES_SHEET_NAME,
            data: JSON.stringify(saleData),
            id: editingSaleId
        });
        
        if (res.success) {
            showSuccess(editingSaleId ? 'تم تحديث أمر البيع' : 'تم حفظ أمر البيع');
            await loadAllData();
            showPage('sales-page');
            document.getElementById('sale-form')?.reset();
            const itemsBody = document.getElementById('sale-items-body');
            if (itemsBody) itemsBody.innerHTML = '';
            addSaleItemRow();
            calculateSaleTotals();
            editingSaleId = null;
            isEditingSale = false;
        } else {
            showError(res.error || 'فشل الحفظ');
        }
    } catch (err) {
        console.error('خطأ في حفظ أمر البيع:', err);
        showError('خطأ في الاتصال: ' + err.message);
    } finally {
        if (btn) {
            btn.innerHTML = originalText;
            btn.disabled = false;
        }
        isSavingSale = false;
    }
}

async function saveComplaint(e) {
    e.preventDefault();
    if (isSavingComplaint) return;
    isSavingComplaint = true;

    const btn = document.getElementById('save-complaint-btn');
    const originalText = btn?.innerHTML;
    if (btn) {
        btn.innerHTML = '<i class="ri-loader-4-line animate-spin"></i> جاري حفظ الشكوى...';
        btn.disabled = true;
    }

    try {
        const date = document.getElementById('complaint-date')?.value;
        const clientSelect = document.getElementById('complaint-client-select');
        const clientName = clientSelect?.options[clientSelect.selectedIndex]?.text || '';
        if (!date || !clientName) { 
            showError('التاريخ والعميل مطلوبان'); 
            return; 
        }

        const attachments = document.getElementById('complaint-attachments');
        let attachmentUrls = [];
        if (attachments && attachments.files.length > 0) {
            for (let file of attachments.files) {
                const base64 = await new Promise((resolve) => {
                    const reader = new FileReader();
                    reader.onload = () => resolve(reader.result.split(',')[1]);
                    reader.readAsDataURL(file);
                });
                const uploadRes = await sendRequest({
                    action: 'UPLOAD_FILE',
                    attachment: base64,
                    filename: file.name,
                    mimeType: file.type
                });
                if (uploadRes.success && (uploadRes.data?.url || uploadRes.url)) {
                    attachmentUrls.push(uploadRes.data?.url || uploadRes.url);
                }
            }
        }

        const complaintData = {
            'معرف': await generateSequentialId('CMP', SHEET_CONFIG.COMPLAINTS_SHEET_NAME),
            'التاريخ': date,
            'العميل': clientName,
            'رقم_الهاتف': document.getElementById('complaint-phone')?.value.trim() || '',
            'البريد_الإلكتروني': document.getElementById('complaint-email')?.value.trim() || '',
            'مسؤول_التواصل': document.getElementById('complaint-contact-person')?.value.trim() || '',
            'رقم_مسؤول_التواصل': document.getElementById('complaint-contact-phone')?.value.trim() || '',
            'الكمية': document.getElementById('complaint-qty')?.value || '',
            'الوحدة': document.getElementById('complaint-unit')?.value || '',
            'النوع': document.getElementById('complaint-type')?.value || '',
            'طريقة_الشكوى': document.getElementById('complaint-method')?.value || '',
            'الوصف': document.getElementById('complaint-description')?.value.trim() || '',
            'المرفق': attachmentUrls.join(','),
            'الموظف': currentUser.username,
            'الحالة': 'قيد الاعتماد'
        };

        const res = await sendRequest({
            action: 'ADD',
            sheetName: SHEET_CONFIG.COMPLAINTS_SHEET_NAME,
            data: JSON.stringify(complaintData)
        });
        
        if (res.success) {
            showSuccess('تم حفظ الشكوى');
            await loadAllData();
            showPage('complaints-page');
            document.getElementById('complaint-form')?.reset();
        } else {
            showError(res.error || 'فشل الحفظ');
        }
    } catch (err) {
        showError('خطأ في الاتصال: ' + err.message);
    } finally {
        if (btn) {
            btn.innerHTML = originalText;
            btn.disabled = false;
        }
        isSavingComplaint = false;
    }
}

async function saveCollection(e) {
    e.preventDefault();
    if (isSavingCollection) return;
    isSavingCollection = true;

    const btn = document.getElementById('save-collection-btn');
    const originalText = btn?.innerHTML;
    if (btn) {
        btn.innerHTML = '<i class="ri-loader-4-line animate-spin"></i> جاري حفظ التحصيل...';
        btn.disabled = true;
    }

    try {
        const date = document.getElementById('collection-date')?.value;
        const clientSelect = document.getElementById('collection-client-select');
        const clientName = clientSelect?.options[clientSelect.selectedIndex]?.text || '';
        const amount = document.getElementById('collection-amount')?.value;
        if (!date || !clientName || !amount) { 
            showError('التاريخ والعميل والمبلغ مطلوبة'); 
            return; 
        }

        const collectionData = {
            'معرف': await generateSequentialId('COL', SHEET_CONFIG.COLLECTIONS_SHEET_NAME),
            'التاريخ': date,
            'العميل': clientName,
            'المبلغ_المستحق': amount,
            'تاريخ_الاستحقاق': document.getElementById('collection-due')?.value || '',
            'الحالة': document.getElementById('collection-status')?.value || '',
            'ملاحظات': document.getElementById('collection-notes')?.value.trim() || '',
            'الموظف': currentUser.username
        };

        const res = await sendRequest({
            action: 'ADD',
            sheetName: SHEET_CONFIG.COLLECTIONS_SHEET_NAME,
            data: JSON.stringify(collectionData)
        });
        
        if (res.success) {
            showSuccess('تم حفظ التحصيل');
            await loadAllData();
            showPage('collections-page');
            document.getElementById('collection-form')?.reset();
        } else {
            showError(res.error || 'فشل الحفظ');
        }
    } catch (err) {
        showError('خطأ في الاتصال: ' + err.message);
    } finally {
        if (btn) {
            btn.innerHTML = originalText;
            btn.disabled = false;
        }
        isSavingCollection = false;
    }
}

// ═══════════════════════════════════════════════════════════════════════════
// القسم السادس: دوال التعديل والحذف
// ═══════════════════════════════════════════════════════════════════════════
// ==============================================
// دالة تعديل عرض السعر (editQuote)
// ==============================================

function editQuote(id) {
    // البحث عن عرض السعر في البيانات المخزنة مؤقتاً
    const quote = appCache.data.quotes.find(q => getSafeValue(q, 'معرف') == id);
    if (!quote) {
        showError('عرض السعر غير موجود');
        return;
    }
    
    // التحقق من حالة عرض السعر (لا يمكن تعديل المعتمد)
    const status = getSafeValue(quote, 'الحالة');
    if (status === 'معتمد') {
        showError('لا يمكن تعديل عرض سعر معتمد');
        return;
    }
    
    // تعيين متغيرات التعديل
    isEditingQuote = true;
    editingQuoteId = id;
    
    // تعبئة التاريخ
    const dateField = document.getElementById('quote-date');
    if (dateField) {
        const quoteDate = getSafeValue(quote, 'التاريخ');
        if (quoteDate) {
            dateField.value = quoteDate.split('T')[0] || quoteDate;
        } else {
            dateField.value = new Date().toISOString().split('T')[0];
        }
    }
    
    // تعبئة اسم العميل
    const clientName = getSafeValue(quote, 'العميل');
    const clientSelect = document.getElementById('quote-client-select');
    if (clientSelect && clientName) {
        // البحث عن العميل في القائمة المنسدلة
        let found = false;
        for (let i = 0; i < clientSelect.options.length; i++) {
            if (clientSelect.options[i].text === clientName) {
                clientSelect.selectedIndex = i;
                found = true;
                break;
            }
        }
        
        // إذا لم يتم العثور على العميل، نضيفه كخيار جديد
        if (!found) {
            const option = document.createElement('option');
            option.value = clientName;
            option.text = clientName;
            clientSelect.appendChild(option);
            clientSelect.value = clientName;
        }
        
        // تحديث حقل البحث في القائمة المنسدلة
        const wrapper = clientSelect.parentElement?.querySelector('.searchable-wrapper');
        if (wrapper) {
            const searchInput = wrapper.querySelector('input[type="text"]');
            if (searchInput) {
                searchInput.value = clientName;
            }
        }
    }
    
    // تعبئة طريقة السداد
    const paymentMethod = getSafeValue(quote, 'طريقة_السداد');
    const paymentMethodField = document.getElementById('quote-payment-method');
    if (paymentMethodField && paymentMethod) {
        paymentMethodField.value = paymentMethod;
    }
    
    // تعبئة مكان التسليم
    const deliveryPlace = getSafeValue(quote, 'مكان_التسليم');
    const deliveryPlaceField = document.getElementById('quote-delivery-place');
    if (deliveryPlaceField && deliveryPlace) {
        deliveryPlaceField.value = deliveryPlace;
    }
    
    // تعبئة مدة العرض
    const validity = getSafeValue(quote, 'مدة_العرض');
    const validityField = document.getElementById('quote-validity');
    if (validityField && validity) {
        validityField.value = validity;
    }
    
    // تعبئة الملاحظات
    const notes = getSafeValue(quote, 'ملاحظات');
    const notesField = document.getElementById('quote-notes');
    if (notesField && notes) {
        notesField.value = notes;
    }
    
    // تعبئة نوع الضريبة
    const taxType = getSafeValue(quote, 'نوع_الضريبة');
    if (taxType === 'inclusive') {
        const inclusiveRadio = document.querySelector('input[name="taxTypeQuote"][value="inclusive"]');
        if (inclusiveRadio) inclusiveRadio.checked = true;
    } else {
        const exclusiveRadio = document.querySelector('input[name="taxTypeQuote"][value="exclusive"]');
        if (exclusiveRadio) exclusiveRadio.checked = true;
    }
    
    // تعبئة جدول الأصناف
    let items = [];
    try {
        const itemsRaw = getSafeValue(quote, 'تفاصيل_الأصناف');
        items = typeof itemsRaw === 'string' ? JSON.parse(itemsRaw) : (itemsRaw || []);
        if (!Array.isArray(items)) items = [];
    } catch(e) {
        console.error('خطأ في تحليل الأصناف:', e);
        items = [];
    }
    
    const itemsBody = document.getElementById('quote-items-body');
    if (itemsBody) {
        // مسح الجدول الحالي
        itemsBody.innerHTML = '';
        
        if (items.length === 0) {
            // إضافة صف فارغ إذا لم توجد أصناف
            addQuoteItemRow();
        } else {
            // إضافة الأصناف الموجودة
            items.forEach(item => {
                addQuoteItemRow(
                    item.code || '',
                    item.name || '',
                    item.qty || '',
                    item.unit || '',
                    item.unitPrice || '',
                    item.total || ''
                );
            });
        }
    }
    
    // إعادة حساب الإجماليات
    calculateQuoteTotals();
    
    // الانتقال إلى صفحة التعديل
    showPage('add-quote-page');
    
    // عرض رسالة تأكيد
    showSuccess('جاري تعديل عرض السعر رقم: ' + id);
}

// ==============================================
// دالة إضافة صف جديد في جدول عروض الأسعار (مع دعم البيانات الموجودة)
// ==============================================

function addQuoteItemRow(code = '', name = '', qty = '', unit = '', unitPrice = '', total = '') {
    const tbody = document.getElementById('quote-items-body');
    if (!tbody) return;
    
    const row = document.createElement('tr');
    const rowCount = tbody.children.length + 1;
    
    row.innerHTML = `
        <td class="text-center font-bold text-gray-700" style="width: 5%">${rowCount}</td>
        <td style="width: 15%">
            <select class="quote-item-code w-full px-3 py-2 border border-gray-300 rounded-lg text-sm focus:border-primary focus:ring-2 focus:ring-primary/20" 
                    onchange="updateQuoteItemName(this); calculateQuoteTotals();">
                ${getItemsOptions(code)}
            </select>
        </td>
        <td style="width: 20%">
            <input type="text" class="quote-item-name w-full px-3 py-2 border border-gray-300 rounded-lg text-sm bg-gray-50" 
                   value="${name.replace(/"/g, '&quot;')}" placeholder="اسم الصنف" readonly>
        </td>
        <td style="width: 8%">
            <input type="number" class="quote-qty w-full px-3 py-2 border border-gray-300 rounded-lg text-sm text-center" 
                   value="${qty}" placeholder="0" min="0" step="0.01" 
                   onchange="calculateQuoteTotals()" oninput="calculateQuoteTotals()">
        </td>
        <td style="width: 10%">
            <select class="quote-unit w-full px-3 py-2 border border-gray-300 rounded-lg text-sm" onchange="calculateQuoteTotals()">
                <option value="">اختر</option>
                <option value="كيلو" ${unit === 'كيلو' ? 'selected' : ''}>كيلو</option>
                <option value="طن" ${unit === 'طن' ? 'selected' : ''}>طن</option>
                <option value="متر" ${unit === 'متر' ? 'selected' : ''}>متر</option>
                <option value="متر مربع" ${unit === 'متر مربع' ? 'selected' : ''}>متر مربع</option>
                <option value="عدد" ${unit === 'عدد' ? 'selected' : ''}>عدد</option>
            </select>
        </td>
        <td style="width: 12%">
            <input type="number" class="quote-unit-price w-full px-3 py-2 border border-gray-300 rounded-lg text-sm text-left" 
                   value="${unitPrice}" placeholder="0.00" min="0" step="0.01" 
                   onchange="calculateQuoteTotals()" oninput="calculateQuoteTotals()">
        </td>
        <td style="width: 12%">
            <input type="text" class="quote-item-total w-full px-3 py-2 border border-gray-300 rounded-lg text-sm bg-gray-100 text-left font-bold text-primary" 
                   value="${total ? parseFloat(total).toFixed(2) : ''}" readonly placeholder="0.00">
        </td>
        <td style="width: 8%">
            <div class="flex gap-1 justify-center">
                <button type="button" onclick="addQuoteItemRow()" class="text-green-500 hover:text-green-700 hover:bg-green-50 p-1 rounded transition-colors" title="إضافة صف جديد">
                    <i class="ri-add-line text-xl"></i>
                </button>
                <button type="button" onclick="deleteQuoteRow(this)" class="text-red-500 hover:text-red-700 hover:bg-red-50 p-1 rounded transition-colors" title="حذف الصف">
                    <i class="ri-delete-bin-line text-xl"></i>
                </button>
            </div>
        </td>
    `;
    
    tbody.appendChild(row);
    
    // تحديث اسم الصنف إذا كان الكود موجود
    if (code) {
        const codeSelect = row.querySelector('.quote-item-code');
        if (codeSelect) {
            updateQuoteItemName(codeSelect);
        }
    }
    
    // إعادة ترقيم الصفوف
    renumberQuoteRows();
}

// ==============================================
// دالة تحديث اسم الصنف عند اختيار الكود
// ==============================================

function updateQuoteItemName(selectElement) {
    const row = selectElement.closest('tr');
    const nameInput = row.querySelector('.quote-item-name');
    const selectedOption = selectElement.options[selectElement.selectedIndex];
    
    if (selectedOption && selectedOption.dataset.name) {
        nameInput.value = selectedOption.dataset.name;
    } else {
        nameInput.value = '';
    }
    
    // تحديث سعر الوحدة تلقائياً من قائمة الأسعار إذا كان متاحاً
    const selectedCode = selectElement.value;
    if (selectedCode && itemsMap.has(selectedCode)) {
        const item = itemsMap.get(selectedCode);
        const price = getSafeValue(item, 'السعر') || getSafeValue(item, 'price') || 0;
        const unitPriceInput = row.querySelector('.quote-unit-price');
        if (unitPriceInput && price && !unitPriceInput.value) {
            unitPriceInput.value = price;
        }
    }
    
    calculateQuoteTotals();
}

// ==============================================
// دالة حذف صف من جدول عروض الأسعار
// ==============================================

function deleteQuoteRow(btn) {
    const row = btn.closest('tr');
    if (row) {
        const tbody = row.parentElement;
        if (tbody.children.length === 1) {
            // إذا كان هذا هو الصف الوحيد، نقوم بمسح محتواه بدلاً من حذفه
            const inputs = row.querySelectorAll('input, select');
            inputs.forEach(input => {
                if (input.type === 'number' || input.type === 'text') {
                    input.value = '';
                } else if (input.tagName === 'SELECT') {
                    input.selectedIndex = 0;
                }
            });
            // إعادة تعيين اسم الصنف
            const nameInput = row.querySelector('.quote-item-name');
            if (nameInput) nameInput.value = '';
        } else {
            row.remove();
        }
        calculateQuoteTotals();
        renumberQuoteRows();
    }
}

// ==============================================
// دالة إعادة ترقيم صفوف جدول عروض الأسعار
// ==============================================

function renumberQuoteRows() {
    const rows = document.querySelectorAll('#quote-items-body tr');
    rows.forEach((row, index) => {
        const numCell = row.querySelector('td:first-child');
        if (numCell) {
            numCell.textContent = index + 1;
        }
    });
}

// ==============================================
// دالة حساب إجماليات عرض السعر
// ==============================================

function calculateQuoteTotals() {
    const rows = document.querySelectorAll('#quote-items-body tr');
    let subtotal = 0;
    
    rows.forEach(row => {
        const qtyInput = row.querySelector('.quote-qty');
        const priceInput = row.querySelector('.quote-unit-price');
        const totalInput = row.querySelector('.quote-item-total');
        
        const qty = parseFloat(qtyInput?.value) || 0;
        const unitPrice = parseFloat(priceInput?.value) || 0;
        const itemTotal = qty * unitPrice;
        
        if (totalInput) {
            totalInput.value = itemTotal > 0 ? itemTotal.toFixed(2) : '';
        }
        
        subtotal += itemTotal;
    });
    
    // تحديد نوع الضريبة
    const taxType = document.querySelector('input[name="taxTypeQuote"]:checked')?.value || 'exclusive';
    let tax = 0;
    let total = subtotal;
    
    if (taxType === 'exclusive') {
        tax = subtotal * 0.14;
        total = subtotal + tax;
    } else {
        // إذا كان شامل الضريبة، نحسب الضريبة من الإجمالي
        tax = total - (total / 1.14);
    }
    
    // تحديث حقول الإجماليات
    const subtotalEl = document.getElementById('quote-subtotal-before-tax');
    const taxEl = document.getElementById('quote-total-tax');
    const totalEl = document.getElementById('quote-total-amount');
    
    if (subtotalEl) subtotalEl.innerText = subtotal.toFixed(2);
    if (taxEl) taxEl.innerText = tax.toFixed(2);
    if (totalEl) totalEl.innerText = total.toFixed(2);
}

// ==============================================
// دالة الحصول على خيارات الأصناف للقوائم المنسدلة
// ==============================================

function getItemsOptions(selectedCode = '') {
    if (!appCache.data.items?.length) {
        return '<option value="">لا توجد أصناف</option>';
    }
    
    let options = '<option value="">-- اختر كود الصنف --</option>';
    
    appCache.data.items.forEach(item => {
        const code = getSafeValue(item, 'الكود') || getSafeValue(item, 'code') || '';
        const name = getSafeValue(item, 'الاسم') || getSafeValue(item, 'name') || '';
        if (code) {
            const selected = (code === selectedCode) ? 'selected' : '';
            options += `<option value="${code.replace(/"/g, '&quot;')}" data-name="${name.replace(/"/g, '&quot;')}" ${selected}>${code} - ${name}</option>`;
        }
    });
    
    return options;
}


function editCustomer(id) {
    const customer = appCache.data.customers.find(c => getSafeValue(c, 'معرف') == id);
    if (!customer) return;
    
    const status = getSafeValue(customer, 'الحالة');
    if (status === 'معتمد') {
        showError('لا يمكن تعديل عميل معتمد');
        return;
    }
    
    originalCustomerStatus = status;
    
    isEditingCustomer = true;
    editingCustomerId = id;
    
    const idField = document.getElementById('customer-id');
    const nameField = document.getElementById('customer-name');
    const typeField = document.getElementById('customer-type');
    const phoneField = document.getElementById('customer-phone');
    const emailField = document.getElementById('customer-email');
    const addressField = document.getElementById('customer-address');
    const notesField = document.getElementById('customer-notes');
    const contactPersonField = document.getElementById('customer-contact-person');
    const contactPhoneField = document.getElementById('customer-contact-phone');
    const taxCardField = document.getElementById('customer-tax-card');
    const idCardField = document.getElementById('customer-id-card');
    const passportField = document.getElementById('customer-passport');
    
    if (idField) idField.value = id;
    if (nameField) nameField.value = getSafeValue(customer, 'اسم_العميل') || getSafeValue(customer, 'اسم العميل');
    if (typeField) typeField.value = getSafeValue(customer, 'نوع_العميل') || '';
    if (phoneField) phoneField.value = getSafeValue(customer, 'رقم_الهاتف');
    if (emailField) emailField.value = getSafeValue(customer, 'البريد_الإلكتروني');
    if (addressField) addressField.value = getSafeValue(customer, 'العنوان');
    if (notesField) notesField.value = getSafeValue(customer, 'الملاحظات');
    if (contactPersonField) contactPersonField.value = getSafeValue(customer, 'مسؤول_العميل');
    if (contactPhoneField) contactPhoneField.value = getSafeValue(customer, 'هاتف_مسؤول_العميل');
    if (taxCardField) taxCardField.value = getSafeValue(customer, 'البطاقة_الضريبية');
    if (idCardField) idCardField.value = getSafeValue(customer, 'البطاقة_الشخصية');
    if (passportField) passportField.value = getSafeValue(customer, 'الباسبور');
    
    // إظهار الحقل المناسب حسب نوع العميل
    toggleCustomerCardFields();
    
    showPage('add-customer-page');
}


function deleteCustomer(id) {
    const customer = appCache.data.customers.find(c => getSafeValue(c, 'معرف') == id);
    if (!customer) return;
    
    const status = getSafeValue(customer, 'الحالة');
    if (status === 'معتمد') {
        showError('لا يمكن حذف عميل معتمد');
        return;
    }
    
    if (!confirm('هل أنت متأكد من حذف هذا العميل؟')) return;
    
    sendRequest({
        action: 'DELETE',
        sheetName: SHEET_CONFIG.CUSTOMERS_SHEET_NAME,
        id: id
    }).then(res => {
        if (res.success) {
            showSuccess('تم حذف العميل');
            loadAllData(true);
        } else {
            showError(res.error || 'فشل الحذف');
        }
    });
}

function deleteQuote(id) {
    const quote = appCache.data.quotes.find(q => getSafeValue(q, 'معرف') == id);
    if (!quote) return;
    
    const status = getSafeValue(quote, 'الحالة');
    if (status === 'معتمد') {
        showError('لا يمكن حذف عرض سعر معتمد');
        return;
    }
    
    if (!confirm('هل أنت متأكد من حذف عرض السعر؟')) return;
    
    sendRequest({
        action: 'DELETE',
        sheetName: SHEET_CONFIG.QUOTES_SHEET_NAME,
        id: id
    }).then(res => {
        if (res.success) {
            showSuccess('تم حذف عرض السعر');
            loadAllData(true);
        } else {
            showError(res.error || 'فشل الحذف');
        }
    });
}

function editSale(id) {
    const sale = appCache.data.sales.find(s => getSafeValue(s, 'معرف') == id);
    if (!sale) return;
    
    const status = getSafeValue(sale, 'الحالة');
    if (status === 'معتمد') {
        showError('لا يمكن تعديل أمر بيع معتمد');
        return;
    }
    
    isEditingSale = true;
    editingSaleId = id;
    
    const idField = document.getElementById('sale-id');
    const dateField = document.getElementById('sale-date');
    const clientSelect = document.getElementById('sale-client-select');
    
    if (idField) idField.value = id;
    if (dateField) dateField.value = formatDate(getSafeValue(sale, 'التاريخ'), true);
    
    const clientName = getSafeValue(sale, 'العميل');
    if (clientSelect) {
        for (let i = 0; i < clientSelect.options.length; i++) {
            if (clientSelect.options[i].text === clientName) {
                clientSelect.selectedIndex = i;
                break;
            }
        }
    }
    
    let items = [];
    try {
        items = JSON.parse(getSafeValue(sale, 'تفاصيل_الأصناف') || '[]');
    } catch(e) { items = []; }
    
    const itemsBody = document.getElementById('sale-items-body');
    if (itemsBody) {
        itemsBody.innerHTML = '';
        items.forEach(item => {
            addSaleItemRow(item.code, item.name, item.qty, item.unit, item.unitPrice, item.discount, item.total);
        });
        if (items.length === 0) addSaleItemRow();
    }
    
    calculateSaleTotals();
    
    const manLoc = document.getElementById('sale-manufacturing-location');
    const payMethod = document.getElementById('sale-payment-method');
    const delPlace = document.getElementById('sale-delivery-place');
    const terms = document.getElementById('terms-conditions');
    const notes = document.getElementById('sale-notes');
    
    if (manLoc) manLoc.value = getSafeValue(sale, 'مكان_التصنيع');
    if (payMethod) payMethod.value = getSafeValue(sale, 'طريقة_السداد');
    if (delPlace) delPlace.value = getSafeValue(sale, 'مكان_التسليم');
    if (terms) terms.value = getSafeValue(sale, 'الشروط_والأحكام');
    if (notes) notes.value = getSafeValue(sale, 'الملاحظات');
    
    showPage('add-sales-page');
}

function deleteSale(id) {
    const sale = appCache.data.sales.find(s => getSafeValue(s, 'معرف') == id);
    if (!sale) return;
    
    const status = getSafeValue(sale, 'الحالة');
    if (status === 'معتمد') {
        showError('لا يمكن حذف أمر بيع معتمد');
        return;
    }
    
    if (!confirm('هل أنت متأكد من حذف أمر البيع؟')) return;
    
    sendRequest({
        action: 'DELETE',
        sheetName: SHEET_CONFIG.SALES_SHEET_NAME,
        id: id
    }).then(res => {
        if (res.success) {
            showSuccess('تم حذف أمر البيع');
            loadAllData(true);
        } else {
            showError(res.error || 'فشل الحذف');
        }
    });
}

// ═══════════════════════════════════════════════════════════════════════════
// القسم السابع: دوال إضافة الصفوف الديناميكية
// ═══════════════════════════════════════════════════════════════════════════

function addActivityRow(
    clientName = '', 
    address = '', 
    phone = '', 
    subject = '', 
    whatDone = '', 
    salesToday = '', 
    collectionToday = '', 
    fromTime = '', 
    toTime = ''
) {
    const tbody = document.getElementById('activities-detail-body');
    if (!tbody) return;
    
    const rowCount = tbody.children.length + 1;
    const row = document.createElement('tr');
    row.className = 'border-b border-gray-100 hover:bg-gray-50 transition-colors';
    
    // الحصول على قائمة العملاء للقائمة المنسدلة
    let customersList = [];
    if (currentUser) {
        customersList = (appCache.data.customers || []).filter(c => {
            if (currentUser.role === 'admin' || currentUser.role === 'manager') return true;
            return usernameMatches(getSafeValue(c, 'الموظف'), currentUser.username);
        }).map(c => ({
            name: getSafeValue(c, 'اسم_العميل') || getSafeValue(c, 'اسم العميل'),
            address: getSafeValue(c, 'العنوان') || '',
            phone: getSafeValue(c, 'رقم_الهاتف') || ''
        }));
    }
    
    // إضافة العميل الحالي إذا لم يكن موجوداً
    if (clientName && !customersList.some(c => c.name === clientName)) {
        customersList.unshift({ name: clientName, address: address, phone: phone });
    }
    
    let clientOptions = '<option value="">-- اختر عميلاً --</option>';
    customersList.forEach(c => {
        const selected = (c.name === clientName) ? 'selected' : '';
        clientOptions += `<option value="${c.name.replace(/"/g, '&quot;')}" data-address="${c.address.replace(/"/g, '&quot;')}" data-phone="${c.phone}" ${selected}>${c.name}</option>`;
    });
    
    row.innerHTML = `
        <td class="px-4 py-3 text-center font-bold text-gray-700 border-b">${rowCount}</td>
        <td class="px-4 py-3 border-b">
            <select class="activity-client w-full px-3 py-2 border border-gray-300 rounded-lg text-sm focus:border-primary focus:ring-2 focus:ring-primary/20" 
                    onchange="updateClientInfo(this)">
                ${clientOptions}
            </select>
        </td>
        <td class="px-4 py-3 border-b">
            <input type="text" class="activity-address w-full px-3 py-2 border border-gray-300 rounded-lg text-sm" 
                   placeholder="العنوان" value="${address.replace(/"/g, '&quot;')}">
        </td>
        <td class="px-4 py-3 border-b">
            <input type="tel" class="activity-phone w-full px-3 py-2 border border-gray-300 rounded-lg text-sm text-left" 
                   placeholder="رقم الهاتف" value="${phone}" dir="ltr">
        </td>
        <td class="px-4 py-3 border-b">
            <input type="text" class="activity-subject w-full px-3 py-2 border border-gray-300 rounded-lg text-sm" 
                   placeholder="الموضوع" value="${subject.replace(/"/g, '&quot;')}">
        </td>
        <td class="px-4 py-3 border-b">
            <textarea class="activity-what-done w-full px-3 py-2 border border-gray-300 rounded-lg text-sm resize-none" 
                      rows="2" placeholder="ما تم...">${whatDone.replace(/"/g, '&quot;')}</textarea>
        </td>
        <td class="px-4 py-3 border-b">
            <input type="number" class="activity-sales w-full px-3 py-2 border border-gray-300 rounded-lg text-sm text-left" 
                   placeholder="0.00" value="${salesToday}" step="0.01" min="0" 
                   oninput="calculateActivityTotals()">
        </td>
        <td class="px-4 py-3 border-b">
            <input type="number" class="activity-collection w-full px-3 py-2 border border-gray-300 rounded-lg text-sm text-left" 
                   placeholder="0.00" value="${collectionToday}" step="0.01" min="0" 
                   oninput="calculateActivityTotals()">
        </td>
        <td class="px-4 py-3 border-b">
            <input type="time" class="activity-from-time w-full px-3 py-2 border border-gray-300 rounded-lg text-sm text-center" 
                   value="${fromTime}" step="60">
        </td>
        <td class="px-4 py-3 border-b">
            <input type="time" class="activity-to-time w-full px-3 py-2 border border-gray-300 rounded-lg text-sm text-center" 
                   value="${toTime}" step="60">
        </td>
        <td class="px-4 py-3 border-b text-center whitespace-nowrap">
            <div class="flex gap-1 justify-center">
                <button type="button" onclick="addActivityRow()" class="text-green-500 hover:text-green-700 hover:bg-green-50 p-1 rounded transition-colors" title="إضافة صف جديد">
                    <i class="ri-add-line text-xl"></i>
                </button>
                <button type="button" onclick="deleteActivityRow(this)" class="text-red-500 hover:text-red-700 hover:bg-red-50 p-1 rounded transition-colors" title="حذف الصف">
                    <i class="ri-delete-bin-line text-xl"></i>
                </button>
            </div>
        </td>
    `;
    
    tbody.appendChild(row);
    
    // تحديث معلومات العميل تلقائياً إذا تم اختيار عميل
    const clientSelect = row.querySelector('.activity-client');
    if (clientSelect && clientName) {
        const selectedOption = Array.from(clientSelect.options).find(opt => opt.value === clientName);
        if (selectedOption) {
            clientSelect.value = clientName;
            updateClientInfo(clientSelect);
        }
    }
    
    // إعادة ترقيم الصفوف وحساب الإجماليات
    renumberActivityRows();
    calculateActivityTotals();
}

function deleteActivityRow(btn) {
    const row = btn.closest('tr');
    if (row) {
        const tbody = row.parentElement;
        if (tbody.children.length === 1) {
            // إذا كان هذا هو الصف الوحيد، نقوم بمسح محتواه بدلاً من حذفه
            const inputs = row.querySelectorAll('input, textarea, select');
            inputs.forEach(input => {
                if (input.type === 'number') {
                    input.value = '';
                } else if (input.type === 'text' || input.type === 'tel' || input.tagName === 'TEXTAREA') {
                    input.value = '';
                } else if (input.type === 'date') {
                    input.value = '';
                } else if (input.tagName === 'SELECT') {
                    input.selectedIndex = 0;
                }
            });
            // إعادة تعيين العنوان والهاتف
            const addressInput = row.querySelector('.activity-address');
            const phoneInput = row.querySelector('.activity-phone');
            if (addressInput) addressInput.value = '';
            if (phoneInput) phoneInput.value = '';
        } else {
            row.remove();
        }
        renumberActivityRows();
        calculateActivityTotals();
    }
}

function updateClientInfo(selectElement) {
    const row = selectElement.closest('tr');
    const selectedOption = selectElement.options[selectElement.selectedIndex];
    const addressInput = row.querySelector('.activity-address');
    const phoneInput = row.querySelector('.activity-phone');
    
    if (selectedOption && selectedOption.value) {
        const address = selectedOption.getAttribute('data-address') || '';
        const phone = selectedOption.getAttribute('data-phone') || '';
        if (addressInput) addressInput.value = address;
        if (phoneInput) phoneInput.value = phone;
    } else {
        if (addressInput) addressInput.value = '';
        if (phoneInput) phoneInput.value = '';
    }
}

function calculateActivityTotals() {
    const rows = document.querySelectorAll('#activities-detail-body tr');
    let totalSales = 0;
    let totalCollection = 0;
    
    rows.forEach(row => {
        const salesInput = row.querySelector('.activity-sales');
        const collectionInput = row.querySelector('.activity-collection');
        
        const sales = parseFloat(salesInput?.value) || 0;
        const collection = parseFloat(collectionInput?.value) || 0;
        
        totalSales += sales;
        totalCollection += collection;
    });
    
    // تحديث حقول الإجماليات
    const totalSalesEl = document.getElementById('total-sales-today');
    const totalCollectionEl = document.getElementById('total-collection-today');
    
    if (totalSalesEl) totalSalesEl.innerText = totalSales.toFixed(2);
    if (totalCollectionEl) totalCollectionEl.innerText = totalCollection.toFixed(2);
}


function addQuoteItemRow(code = '', name = '', qty = '', unit = '', unitPrice = '', total = '') {
    const tbody = document.getElementById('quote-items-body');
    if (!tbody) return;
    const row = document.createElement('tr');
    const rowCount = tbody.children.length + 1;
    
    row.innerHTML = `
        <td class="text-center font-bold text-gray-700">${rowCount}</td>
        <td>
            <select class="quote-item-code w-full px-2 py-1 border border-gray-300 rounded-lg text-sm focus:border-primary focus:ring-2 focus:ring-primary/20" 
                    onchange="updateQuoteItemName(this); calculateQuoteTotals();">
                ${getItemsOptions(code)}
            </select>
        </td>
        <td>
            <input type="text" class="quote-item-name w-full px-2 py-1 border border-gray-300 rounded-lg text-sm bg-gray-50" 
                   value="${name.replace(/"/g, '&quot;')}" placeholder="اسم الصنف" readonly>
        </td>
        <td>
            <input type="number" class="quote-qty w-full px-2 py-1 border border-gray-300 rounded-lg text-sm text-center" 
                   value="${qty}" placeholder="0" min="0" step="0.01" 
                   onchange="calculateQuoteTotals()" oninput="calculateQuoteTotals()">
        </td>
        <td>
            <select class="quote-unit w-full px-2 py-1 border border-gray-300 rounded-lg text-sm" onchange="calculateQuoteTotals()">
                <option value="">اختر</option>
                <option value="كيلو" ${unit === 'كيلو' ? 'selected' : ''}>كيلو</option>
                <option value="طن" ${unit === 'طن' ? 'selected' : ''}>طن</option>
                <option value="متر" ${unit === 'متر' ? 'selected' : ''}>متر</option>
                <option value="متر مربع" ${unit === 'متر مربع' ? 'selected' : ''}>متر مربع</option>
                <option value="عدد" ${unit === 'عدد' ? 'selected' : ''}>عدد</option>
            </select>
        </td>
        <td>
            <input type="number" class="quote-unit-price w-full px-2 py-1 border border-gray-300 rounded-lg text-sm text-left" 
                   value="${unitPrice}" placeholder="0.00" min="0" step="0.01" 
                   onchange="calculateQuoteTotals()" oninput="calculateQuoteTotals()">
        </td>
        <td>
            <input type="text" class="quote-item-total w-full px-2 py-1 border border-gray-300 rounded-lg text-sm bg-gray-100 text-left font-bold text-primary" 
                   value="${total ? parseFloat(total).toFixed(2) : ''}" readonly placeholder="0.00">
        </td>
        <td>
            <div class="flex gap-1 justify-center">
                <button type="button" onclick="addQuoteItemRow()" class="text-green-500 hover:text-green-700 hover:bg-green-50 p-1 rounded transition-colors" title="إضافة صف جديد">
                    <i class="ri-add-line text-xl"></i>
                </button>
                <button type="button" onclick="deleteQuoteRow(this)" class="text-red-500 hover:text-red-700 hover:bg-red-50 p-1 rounded transition-colors" title="حذف الصف">
                    <i class="ri-delete-bin-line text-xl"></i>
                </button>
            </div>
        </td>
    `;
    
    tbody.appendChild(row);
    
    if (code) {
        updateQuoteItemName(row.querySelector('.quote-item-code'));
    }
    
    calculateQuoteTotals();
    renumberQuoteRows();
}

function renumberQuoteRows() {
    const rows = document.querySelectorAll('#quote-items-body tr');
    rows.forEach((row, index) => {
        const numCell = row.querySelector('td:first-child');
        if (numCell) {
            numCell.textContent = index + 1;
        }
    });
}

function addSaleItemRow(code = '', name = '', qty = '', unit = '', unitPrice = '', discount = '0', total = '') {
    const tbody = document.getElementById('sale-items-body');
    if (!tbody) return;
    const row = document.createElement('tr');
    const rowCount = tbody.children.length + 1;
    row.innerHTML = `
        <td class="text-center font-bold">${rowCount}</td>
        <td>
            <select class="sale-item-code w-full px-2 py-1 border rounded" onchange="updateSaleItemName(this)">
                ${getItemsOptions(code)}
            </select>
        </td>
        <td><input type="text" class="sale-item-name w-full px-2 py-1 border rounded" value="${name.replace(/"/g, '&quot;')}" placeholder="اسم الصنف" readonly style="background:#f9fafb;"></td>
        <td><input type="number" class="sale-qty w-full px-2 py-1 border rounded" value="${qty}" placeholder="الكمية" onchange="calculateSaleTotals()"></td>
        <td>
            <select class="sale-unit w-full px-2 py-1 border rounded">
                <option value="">اختر</option>
                <option value="كيلو" ${unit === 'كيلو' ? 'selected' : ''}>كيلو</option>
                <option value="طن" ${unit === 'طن' ? 'selected' : ''}>طن</option>
                <option value="متر" ${unit === 'متر' ? 'selected' : ''}>متر</option>
                <option value="متر مربع" ${unit === 'متر مربع' ? 'selected' : ''}>متر مربع</option>
                <option value="عدد" ${unit === 'عدد' ? 'selected' : ''}>عدد</option>
            </select>
        </td>
        <td><input type="number" class="sale-unit-price w-full px-2 py-1 border rounded" value="${unitPrice}" placeholder="السعر" onchange="calculateSaleTotals()"></td>
        <td><input type="number" class="sale-discount w-full px-2 py-1 border rounded" value="${discount}" placeholder="%" onchange="calculateSaleTotals()"></td>
        <td><input type="text" class="sale-item-total w-full px-2 py-1 border rounded bg-gray-100" value="${total}" readonly></td>
        <td>
            <div class="flex gap-1 justify-center">
                <button type="button" onclick="addSaleItemRow()" class="text-green-500 hover:text-green-700 p-1" title="إضافة صف جديد">
                    <i class="ri-add-line text-xl"></i>
                </button>
                <button type="button" onclick="this.closest('tr').remove(); calculateSaleTotals(); renumberSaleRows();" class="text-red-500 hover:text-red-700 p-1" title="حذف الصف">
                    <i class="ri-delete-bin-line text-xl"></i>
                </button>
            </div>
        </td>
    `;
    tbody.appendChild(row);
    if (code) {
        updateSaleItemName(row.querySelector('.sale-item-code'));
    }
    calculateSaleTotals();
    renumberSaleRows();
}

function renumberSaleRows() {
    const rows = document.querySelectorAll('#sale-items-body tr');
    rows.forEach((row, index) => {
        const firstTd = row.querySelector('td:first-child');
        if (firstTd) firstTd.textContent = index + 1;
    });
}

function updateSaleItemName(selectElement) {
    const row = selectElement.closest('tr');
    const nameInput = row.querySelector('.sale-item-name');
    const selectedOption = selectElement.options[selectElement.selectedIndex];
    if (selectedOption && selectedOption.dataset.name) {
        nameInput.value = selectedOption.dataset.name;
    } else {
        nameInput.value = '';
    }
    calculateSaleTotals();
}

function calculateSaleTotals() {
    const rows = document.querySelectorAll('#sale-items-body tr');
    let subtotal = 0;
    
    rows.forEach(row => {
        const qty = parseFloat(row.querySelector('.sale-qty')?.value) || 0;
        const unitPrice = parseFloat(row.querySelector('.sale-unit-price')?.value) || 0;
        const discount = parseFloat(row.querySelector('.sale-discount')?.value) || 0;
        
        const itemTotal = qty * unitPrice * (1 - discount / 100);
        const totalInput = row.querySelector('.sale-item-total');
        if (totalInput) totalInput.value = itemTotal.toFixed(2);
        subtotal += itemTotal;
    });
    
    const taxType = document.querySelector('input[name="taxType"]:checked')?.value || 'exclusive';
    let tax = 0;
    let total = subtotal;
    
    if (taxType === 'exclusive') {
        tax = subtotal * 0.14;
        total = subtotal + tax;
    } else {
        tax = total - (total / 1.14);
    }
    
    const subtotalEl = document.getElementById('subtotal-before-tax');
    const taxEl = document.getElementById('sale-total-tax');
    const totalEl = document.getElementById('sale-total-amount');
    
    if (subtotalEl) subtotalEl.innerText = subtotal.toFixed(2);
    if (taxEl) taxEl.innerText = tax.toFixed(2);
    if (totalEl) totalEl.innerText = total.toFixed(2);
}

function updateQuoteItemName(selectElement) {
    const row = selectElement.closest('tr');
    const nameInput = row.querySelector('.quote-item-name');
    const selectedOption = selectElement.options[selectElement.selectedIndex];
    if (selectedOption && selectedOption.dataset.name) {
        nameInput.value = selectedOption.dataset.name;
    } else {
        nameInput.value = '';
    }
}

function calculateQuoteTotals() {
    const rows = document.querySelectorAll('#quote-items-body tr');
    let subtotal = 0;
    
    rows.forEach((row, index) => {
        const qtyInput = row.querySelector('.quote-qty');
        const priceInput = row.querySelector('.quote-unit-price');
        const totalInput = row.querySelector('.quote-item-total');
        
        const qty = parseFloat(qtyInput?.value) || 0;
        const unitPrice = parseFloat(priceInput?.value) || 0;
        const itemTotal = qty * unitPrice;
        
        if (totalInput) {
            totalInput.value = itemTotal > 0 ? itemTotal.toFixed(2) : '';
        }
        
        subtotal += itemTotal;
    });
    
    const taxType = document.querySelector('input[name="taxTypeQuote"]:checked')?.value || 'exclusive';
    let tax = 0;
    let total = subtotal;
    
    if (taxType === 'exclusive') {
        tax = subtotal * 0.14;
        total = subtotal + tax;
    } else {
        tax = total - (total / 1.14);
    }
    
    const subtotalEl = document.getElementById('quote-subtotal-before-tax');
    const taxEl = document.getElementById('quote-total-tax');
    const totalEl = document.getElementById('quote-total-amount');
    
    if (subtotalEl) subtotalEl.innerText = subtotal.toFixed(2);
    if (taxEl) taxEl.innerText = tax.toFixed(2);
    if (totalEl) totalEl.innerText = total.toFixed(2);
}

function deleteQuoteRow(btn) {
    const row = btn.closest('tr');
    if (row) {
        row.remove();
        calculateQuoteTotals();
        renumberQuoteRows();
    }
}

// ═══════════════════════════════════════════════════════════════════════════
// القسم الثامن: دوال الاعتماد والرفض
// ═══════════════════════════════════════════════════════════════════════════

function toggleAll(type) {
    const cbAll = document.getElementById(`select-all-${type}s`);
    if (!cbAll) return;
    document.querySelectorAll(`.${type}-checkbox`).forEach(cb => cb.checked = cbAll.checked);
}

function toggleAllCustomers() {
    const cbAll = document.getElementById('select-all-customers');
    if (!cbAll) return;
    document.querySelectorAll('.customer-checkbox').forEach(cb => cb.checked = cbAll.checked);
}

async function approveSelected(type) {
    let boxes;
    if (type === 'sale') boxes = document.querySelectorAll('.sale-checkbox:checked');
    else if (type === 'quote') boxes = document.querySelectorAll('.quote-checkbox:checked');
    else if (type === 'complaint') boxes = document.querySelectorAll('.complaint-checkbox:checked');
    
    const ids = Array.from(boxes || []).map(cb => cb.value);
    if (ids.length === 0) return showError('لم يتم تحديد أي مستند');
    
    try {
        const res = await sendRequest({ 
            action: 'UPDATE_DOCUMENT_STATUS', 
            type, 
            ids: JSON.stringify(ids), 
            status: 'معتمد' 
        });
        if (res.success) { 
            showSuccess('تم اعتماد المستندات'); 
            await loadAllData(true); 
        }
        else showError(res.error || 'فشل الاعتماد');
    } catch { 
        showError('خطأ في الاتصال'); 
    }
}

async function rejectSelected(type) {
    let boxes;
    if (type === 'sale') boxes = document.querySelectorAll('.sale-checkbox:checked');
    else if (type === 'quote') boxes = document.querySelectorAll('.quote-checkbox:checked');
    else if (type === 'complaint') boxes = document.querySelectorAll('.complaint-checkbox:checked');
    
    const ids = Array.from(boxes || []).map(cb => cb.value);
    if (ids.length === 0) return showError('لم يتم تحديد أي مستند');
    
    const rejectionType = document.getElementById('rejection-type');
    const rejectionIds = document.getElementById('rejection-ids');
    const rejectionText = document.getElementById('rejection-reason-text');
    const modal = document.getElementById('rejection-reason-modal');
    
    if (rejectionType) rejectionType.value = type;
    if (rejectionIds) rejectionIds.value = JSON.stringify(ids);
    if (rejectionText) rejectionText.value = '';
    if (modal) modal.classList.remove('hidden');
}

async function approveSelectedCustomers() {
    const boxes = document.querySelectorAll('.customer-checkbox:checked');
    const ids = Array.from(boxes).map(cb => cb.value);
    if (ids.length === 0) return showError('لم يتم تحديد أي عميل');
    
    try {
        const res = await sendRequest({ 
            action: 'UPDATE_CUSTOMER_STATUS', 
            ids: JSON.stringify(ids), 
            status: 'معتمد' 
        });
        if (res.success) { 
            showSuccess('تم اعتماد العملاء'); 
            loadAllData(true); 
        }
        else showError(res.error || 'فشل الاعتماد');
    } catch { 
        showError('خطأ في الاتصال'); 
    }
}

async function rejectSelectedCustomers() {
    const boxes = document.querySelectorAll('.customer-checkbox:checked');
    const ids = Array.from(boxes).map(cb => cb.value);
    if (ids.length === 0) return showError('لم يتم تحديد أي عميل');
    
    const rejectionType = document.getElementById('rejection-type');
    const rejectionIds = document.getElementById('rejection-ids');
    const rejectionText = document.getElementById('rejection-reason-text');
    const modal = document.getElementById('rejection-reason-modal');
    
    if (rejectionType) rejectionType.value = 'customer';
    if (rejectionIds) rejectionIds.value = JSON.stringify(ids);
    if (rejectionText) rejectionText.value = '';
    if (modal) modal.classList.remove('hidden');
}

function closeRejectionModal() {
    const modal = document.getElementById('rejection-reason-modal');
    if (modal) modal.classList.add('hidden');
}

async function confirmRejection() {
    const type = document.getElementById('rejection-type')?.value;
    const ids = JSON.parse(document.getElementById('rejection-ids')?.value || '[]');
    const reason = document.getElementById('rejection-reason-text')?.value.trim();
    
    if (!reason) {
        showError('يرجى كتابة سبب الرفض');
        return;
    }
    
    try {
        const res = await sendRequest({ 
            action: type === 'customer' ? 'UPDATE_CUSTOMER_STATUS' : 'UPDATE_DOCUMENT_STATUS', 
            type: type, 
            ids: JSON.stringify(ids), 
            status: 'مرفوض',
            reason: reason
        });
        
        if (res.success) {
            showSuccess('تم رفض المستندات بنجاح');
            closeRejectionModal();
            loadAllData(true);
        } else {
            showError(res.error || 'فشل الرفض');
        }
    } catch(err) {
        showError('خطأ في الاتصال: ' + err.message);
    }
}

function showRejectionReason(reason) {
    if (!reason) {
        showError('لا يوجد سبب مسجل للرفض');
        return;
    }
    const textEl = document.getElementById('view-rejection-text');
    const modal = document.getElementById('view-rejection-modal');
    if (textEl) textEl.textContent = reason;
    if (modal) modal.classList.remove('hidden');
}

// ═══════════════════════════════════════════════════════════════════════════
// القسم التاسع: دوال إدارة المستخدمين
// ═══════════════════════════════════════════════════════════════════════════

function editUser(username) {
    const user = appCache.data.users.find(u => u.username === username);
    if (!user) return;
    
    const origUsername = document.getElementById('edit-original-username');
    const editUsername = document.getElementById('edit-username');
    const editEmail = document.getElementById('edit-email');
    const editPassword = document.getElementById('edit-password');
    const modal = document.getElementById('edit-user-modal');
    
    if (origUsername) origUsername.value = username;
    if (editUsername) editUsername.value = user.username;
    if (editEmail) editEmail.value = user.email;
    if (editPassword) editPassword.value = '';
    
    const roleRadios = document.getElementsByName('edit-role');
    for (let radio of roleRadios) {
        if (radio.value === user.role) {
            radio.checked = true;
            break;
        }
    }
    
    if (modal) modal.classList.remove('hidden');
}

function deleteUser(username) {
    if (!confirm('هل أنت متأكد من حذف هذا المستخدم؟')) return;
    
    sendRequest({
        action: 'DELETE_USER',
        username: username
    }).then(res => {
        if (res.success) {
            showSuccess('تم حذف المستخدم');
            loadAllData(true);
        } else {
            showError(res.error || 'فشل الحذف');
        }
    });
}

async function approveUser(username) {
    if (!confirm(`هل أنت متأكد من اعتماد المستخدم "${username}"؟`)) return;
    
    try {
        const res = await sendRequest({
            action: 'APPROVE_USER',
            username: username
        });
        
        if (res.success) {
            showToast(`تم اعتماد المستخدم ${username} بنجاح`, 'success');
            await loadAllData(true); // إعادة تحميل البيانات
            addNotification(`تم اعتماد حساب المستخدم ${username}`, 'success');
        } else {
            showToast(res.error || 'فشل اعتماد المستخدم', 'error');
        }
    } catch (err) {
        showToast('خطأ في الاتصال: ' + err.message, 'error');
    }
}

async function rejectUser(username) {
    if (!confirm(`هل أنت متأكد من رفض طلب المستخدم "${username}"؟`)) return;
    
    const reason = prompt('سبب الرفض (اختياري):');
    
    try {
        const res = await sendRequest({
            action: 'REJECT_USER',
            username: username,
            reason: reason || ''
        });
        
        if (res.success) {
            showToast(`تم رفض طلب المستخدم ${username}`, 'success');
            await loadAllData(true);
        } else {
            showToast(res.error || 'فشل رفض المستخدم', 'error');
        }
    } catch (err) {
        showToast('خطأ في الاتصال: ' + err.message, 'error');
    }
}

function rejectUser(username) {
    if (!confirm('هل أنت متأكد من رفض هذا المستخدم؟')) return;
    
    sendRequest({
        action: 'REJECT_USER',
        username: username
    }).then(res => {
        if (res.success) {
            showSuccess('تم رفض المستخدم');
            loadAllData(true);
        } else {
            showError(res.error || 'فشل الرفض');
        }
    });
}

// ═══════════════════════════════════════════════════════════════════════════
// القسم العاشر: دوال رسائل المسؤول وقائمة الأسعار
// ═══════════════════════════════════════════════════════════════════════════

function openMessagesModal() {
    const textarea = document.getElementById('admin-messages-textarea');
    if(textarea) textarea.value = adminMessages.join('\n');
    const modal = document.getElementById('messages-modal');
    if(modal) modal.classList.remove('hidden');
}

function closeMessagesModal() {
    const modal = document.getElementById('messages-modal');
    if(modal) modal.classList.add('hidden');
}

function saveMessages() {
    const textarea = document.getElementById('admin-messages-textarea');
    if(textarea) {
        const newMessages = textarea.value.split('\n').map(line => line.trim()).filter(line => line !== '');
        adminMessages = newMessages;
        localStorage.setItem('hyma_adminMessages', JSON.stringify(adminMessages));
        updateMessagesMarquee();
        showSuccess('تم حفظ الرسائل بنجاح');
    }
    closeMessagesModal();
}

function updateMarqueeSpeed() {
    const speedInput = document.getElementById('marquee-speed');
    if(speedInput) {
        let speed = parseInt(speedInput.value);
        if(isNaN(speed) || speed < 5) speed = 5;
        if(speed > 100) speed = 100;
        document.documentElement.style.setProperty('--marquee-duration', speed + 's');
        localStorage.setItem('hyma_marqueeSpeed', speed);
    }
}

function updateMessagesMarquee() {
    const marquee = document.getElementById('message-marquee');
    if(marquee) marquee.innerText = adminMessages.length ? adminMessages.join(' • ') : 'لا توجد رسائل';
}

function openPriceListModal() {
    const modal = document.getElementById('price-list-modal');
    if(modal) modal.classList.remove('hidden');
}

function closePriceListModal() {
    const modal = document.getElementById('price-list-modal');
    if(modal) modal.classList.add('hidden');
}

async function uploadPriceList() {
    const fileInput = document.getElementById('price-list-file');
    const file = fileInput?.files[0];
    if(!file) return showError('يرجى اختيار ملف');
    
    const btn = document.querySelector('#price-list-modal button[onclick="uploadPriceList()"]');
    const originalText = btn?.innerHTML;
    if (btn) {
        btn.innerHTML = '<i class="ri-loader-4-line animate-spin"></i> جاري الرفع...';
        btn.disabled = true;
    }
    
    try {
        const base64Data = await new Promise((resolve, reject) => {
            const reader = new FileReader();
            reader.onload = () => resolve(reader.result.split(',')[1]);
            reader.onerror = reject;
            reader.readAsDataURL(file);
        });

        const res = await sendRequest({
            action: 'UPLOAD_FILE',
            attachment: base64Data,
            filename: file.name,
            mimeType: file.type
        });
        
        if(res.success) {
            let fileUrl = res.data?.url || res.url;
            if (!fileUrl) {
                showError('فشل الحصول على رابط الملف');
                return;
            }
            
            localStorage.setItem('hyma_priceListUrl', fileUrl);
            showSuccess('تم رفع قائمة الأسعار بنجاح');
            closePriceListModal();
        } else {
            showError(res.error || 'فشل رفع الملف');
        }
    } catch(err) {
        showError('خطأ في الاتصال: ' + err.message);
    } finally {
        if (btn) {
            btn.innerHTML = originalText;
            btn.disabled = false;
        }
    }
}

function showPriceList() {
    const url = localStorage.getItem('hyma_priceListUrl');
    if (url) {
        window.open(url, '_blank');
    } else {
        showError('لا توجد قائمة أسعار مرفوعة');
    }
}
// ============================================
// إضافة قائمة منسدلة لزر الخروج في لوحة المسؤول/المدير
// مع إضافة التقارير وإظهار اسم المستخدم والدور الحقيقي
// ============================================
// ============================================
// تعديل دائم: إضافة القائمة المنسدلة للمسؤول/المدير
// ============================================

(function addPermanentAdminDropdown() {
    
    // الانتظار حتى يتم تحميل الصفحة بالكامل
    function initPermanentDropdown() {
        // التأكد من وجود المستخدم وصفحة المسؤول
        if (!currentUser) {
            setTimeout(initPermanentDropdown, 500);
            return;
        }
        
        // التأكد من أننا في صفحة المسؤول/المدير
        const adminPage = document.getElementById('admin-page');
        if (!adminPage || adminPage.classList.contains('hidden')) {
            setTimeout(initPermanentDropdown, 500);
            return;
        }
        
        // البحث عن زر الخروج
        const logoutBtn = document.getElementById('admin-logout');
        if (!logoutBtn) {
            setTimeout(initPermanentDropdown, 500);
            return;
        }
        
        // التحقق إذا كانت القائمة مضافت بالفعل
        if (document.getElementById('admin-profile-btn')) {
            return;
        }
        
        // إخفاء الزر القديم
        logoutBtn.style.display = 'none';
        
        // تحديد الدور والنص المناسب
        const roleText = currentUser.role === 'admin' ? 'مسؤول' : 
                         currentUser.role === 'manager' ? 'مدير' : 'موظف';
        
        const roleIcon = currentUser.role === 'admin' ? 'ri-shield-star-line' : 
                         currentUser.role === 'manager' ? 'ri-team-line' : 'ri-user-line';
        
        // إنشاء القائمة المنسدلة
        const dropdownContainer = document.createElement('div');
        dropdownContainer.className = 'relative';
        
        const dropdownBtn = document.createElement('button');
        dropdownBtn.id = 'admin-profile-btn';
        dropdownBtn.className = 'bg-white/10 hover:bg-white/20 backdrop-blur-sm px-5 py-2.5 rounded-xl transition-all border border-white/10 hover:border-white/30 flex items-center gap-2 font-medium';
        dropdownBtn.innerHTML = `
            <i class="ri-user-settings-line text-xl"></i>
            <span class="hidden md:inline">${currentUser.username}</span>
            <i class="ri-arrow-down-s-line text-sm"></i>
        `;
        
        const dropdownMenu = document.createElement('div');
        dropdownMenu.id = 'admin-profile-dropdown';
        dropdownMenu.className = 'profile-dropdown hidden absolute left-0 mt-2 w-64 bg-white dark:bg-gray-800 rounded-2xl shadow-xl border border-gray-100 dark:border-gray-700 z-50 overflow-hidden';
        dropdownMenu.innerHTML = `
            <div class="px-4 py-3 border-b bg-gradient-to-r from-primary/10 to-primary/5">
                <div class="font-bold text-gray-800 dark:text-white flex items-center gap-2">
                    <i class="${roleIcon} text-primary text-lg"></i>
                    <span id="admin-dropdown-username">${currentUser.username}</span>
                </div>
                <div class="text-xs mt-1">
                    <span class="bg-primary/20 text-primary px-2 py-0.5 rounded-full inline-flex items-center gap-1">
                        <i class="${roleIcon} text-xs"></i>
                        ${roleText}
                    </span>
                </div>
            </div>
            
            <button onclick="showReportsPageFromAdmin()" 
                    class="w-full text-right px-4 py-3 hover:bg-gray-50 dark:hover:bg-gray-700 transition-colors flex items-center gap-3 border-b border-gray-100 dark:border-gray-700">
                <i class="ri-file-list-line text-info text-lg"></i>
                <span class="text-gray-700 dark:text-gray-300 font-medium">التقارير</span>
                <i class="ri-arrow-left-s-line text-gray-400 mr-auto"></i>
            </button>
            
            <button onclick="openEmailModalFromAdmin()" 
                    class="w-full text-right px-4 py-3 hover:bg-gray-50 dark:hover:bg-gray-700 transition-colors flex items-center gap-3 border-b border-gray-100 dark:border-gray-700">
                <i class="ri-mail-send-line text-primary text-lg"></i>
                <span class="text-gray-700 dark:text-gray-300 font-medium">إرسال إيميل</span>
                <i class="ri-arrow-left-s-line text-gray-400 mr-auto"></i>
            </button>
            
            <div class="border-t border-gray-100 dark:border-gray-700 my-1"></div>
            
            <button onclick="logout()" 
                    class="w-full text-right px-4 py-3 hover:bg-red-50 dark:hover:bg-red-900/20 transition-colors flex items-center gap-3">
                <i class="ri-logout-box-r-line text-danger text-lg"></i>
                <span class="text-red-600 dark:text-red-400 font-medium">تسجيل الخروج</span>
                <i class="ri-arrow-left-s-line text-gray-400 mr-auto"></i>
            </button>
        `;
        
        dropdownContainer.appendChild(dropdownBtn);
        dropdownContainer.appendChild(dropdownMenu);
        
        // إضافة الزر الجديد مكان القديم
        logoutBtn.parentNode.insertBefore(dropdownContainer, logoutBtn);
        
        // إضافة الأحداث
        dropdownBtn.addEventListener('click', (e) => {
            e.stopPropagation();
            dropdownMenu.classList.toggle('hidden');
        });
        
        document.addEventListener('click', (e) => {
            if (!dropdownContainer.contains(e.target)) {
                dropdownMenu.classList.add('hidden');
            }
        });
        
        console.log(`✅ تم تثبيت القائمة المنسدلة بشكل دائم للمستخدم: ${currentUser.username}`);
    }
    
    // بدء التهيئة
    if (document.readyState === 'loading') {
        document.addEventListener('DOMContentLoaded', initPermanentDropdown);
    } else {
        initPermanentDropdown();
    }
    
})();

// ============================================
// دوال مساعدة للتقارير والإيميل
// ============================================

function showReportsPageFromAdmin() {
    // إخفاء جميع الصفحات
    document.querySelectorAll('[id$="-page"]').forEach(page => {
        page.classList.add('hidden');
    });
    
    // إظهار صفحة التقارير أو إنشاؤها
    let reportsPage = document.getElementById('reports-page');
    
    if (!reportsPage) {
        createPermanentReportsPage();
        reportsPage = document.getElementById('reports-page');
    }
    
    if (reportsPage) {
        reportsPage.classList.remove('hidden');
        
        // تحديث اسم المستخدم
        const reportsUserName = document.getElementById('reports-user-name');
        if (reportsUserName && currentUser) {
            reportsUserName.textContent = currentUser.username;
        }
        
        // تحميل البيانات
        if (typeof loadAdminReportsData === 'function') {
            loadAdminReportsData();
        } else {
            setTimeout(() => {
                if (typeof applyAdminReportsFilter === 'function') {
                    applyAdminReportsFilter();
                }
            }, 500);
        }
    }
    
    // إغلاق القائمة
    const dropdown = document.getElementById('admin-profile-dropdown');
    if (dropdown) dropdown.classList.add('hidden');
}

function createPermanentReportsPage() {
    const roleText = currentUser?.role === 'admin' ? 'مسؤول' : 
                     currentUser?.role === 'manager' ? 'مدير' : 'موظف';
    
    const reportsHTML = `
        <div id="reports-page" class="hidden min-h-screen flex flex-col bg-gradient-to-br from-gray-50 to-slate-100 dark:from-gray-900 dark:to-gray-800">
            <nav class="bg-gradient-to-r from-primary to-primaryDark text-white shadow-lg fixed w-full top-0 z-50 backdrop-blur-md bg-opacity-95">
                <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
                    <div class="flex items-center gap-3">
                        <button onclick="closePermanentReportsPage()" class="hover:bg-white/20 p-2.5 rounded-xl transition-all">
                            <i class="ri-arrow-right-line text-xl"></i>
                        </button>
                        <h1 class="text-2xl font-bold">التقارير الشاملة</h1>
                    </div>
                    <div class="flex items-center gap-4">
                        <div class="hidden md:flex flex-col items-end">
                            <span id="reports-user-name" class="text-sm font-bold">${currentUser?.username || ''}</span>
                            <span class="text-xs bg-white/20 px-2 py-0.5 rounded-full backdrop-blur-sm">${roleText}</span>
                        </div>
                        <button onclick="closePermanentReportsPage()" class="bg-white/10 hover:bg-white/20 backdrop-blur-sm px-4 py-2 rounded-xl transition-all flex items-center gap-2">
                            <i class="ri-close-line"></i> <span>عودة</span>
                        </button>
                    </div>
                </div>
            </nav>
            
            <main class="flex-1 pt-28 pb-16 px-4">
                <div class="max-w-7xl mx-auto">
                    <div class="bg-white dark:bg-gray-800 rounded-2xl shadow-card p-6 border border-gray-100 dark:border-gray-700 mb-6">
                        <div class="grid grid-cols-1 md:grid-cols-4 gap-4">
                            <div>
                                <label class="block text-sm font-bold text-gray-700 dark:text-gray-300 mb-1">نوع المستند</label>
                                <select id="report-filter-type" class="w-full px-4 py-2 border rounded-xl focus:border-primary dark:bg-gray-900 dark:border-gray-700">
                                    <option value="all">الكل</option>
                                    <option value="أمر بيع">أوامر البيع</option>
                                    <option value="عرض سعر">عروض الأسعار</option>
                                    <option value="شكوى">الشكاوى</option>
                                    <option value="عميل">العملاء</option>
                                    <option value="زيارة">الزيارات</option>
                                    <option value="نشاط يومي">الأنشطة اليومية</option>
                                    <option value="خطة أسبوعية">الخطط الأسبوعية</option>
                                    <option value="تحصيل">التحصيلات</option>
                                </select>
                            </div>
                            <div>
                                <label class="block text-sm font-bold text-gray-700 dark:text-gray-300 mb-1">الحالة</label>
                                <select id="report-filter-status" class="w-full px-4 py-2 border rounded-xl focus:border-primary dark:bg-gray-900 dark:border-gray-700">
                                    <option value="all">الكل</option>
                                    <option value="معتمد">معتمد</option>
                                    <option value="قيد الاعتماد">قيد الاعتماد</option>
                                    <option value="مرفوض">مرفوض</option>
                                </select>
                            </div>
                            <div>
                                <label class="block text-sm font-bold text-gray-700 dark:text-gray-300 mb-1">من تاريخ</label>
                                <input type="date" id="report-filter-date-from" class="w-full px-4 py-2 border rounded-xl dark:bg-gray-900 dark:border-gray-700">
                            </div>
                            <div>
                                <label class="block text-sm font-bold text-gray-700 dark:text-gray-300 mb-1">إلى تاريخ</label>
                                <input type="date" id="report-filter-date-to" class="w-full px-4 py-2 border rounded-xl dark:bg-gray-900 dark:border-gray-700">
                            </div>
                        </div>
                        <div class="flex justify-end mt-4 gap-3">
                            <button onclick="applyPermanentReportsFilter()" class="bg-gradient-to-r from-primary to-primaryDark text-white px-6 py-2 rounded-xl font-bold shadow hover:shadow-lg transition-all">تصفية</button>
                            <button onclick="resetPermanentReportsFilter()" class="bg-gray-200 dark:bg-gray-700 text-gray-700 dark:text-gray-300 px-6 py-2 rounded-xl font-bold">إعادة ضبط</button>
                            <button onclick="exportPermanentReportsToExcel()" class="bg-success text-white px-6 py-2 rounded-xl font-bold flex items-center gap-2"><i class="ri-file-excel-line"></i> تصدير Excel</button>
                        </div>
                    </div>
                    
                    <div id="report-summary" class="mb-4"></div>
                    
                    <div class="table-container overflow-hidden">
                        <div class="overflow-x-auto max-h-[600px] overflow-y-auto">
                            <table class="modern-table w-full min-w-[800px]">
                                <thead class="sticky top-0 z-10 bg-gray-50 dark:bg-gray-800">
                                    <tr>
                                        <th class="px-4 py-3 text-center">النوع</th>
                                        <th class="px-4 py-3 text-center">رقم المستند</th>
                                        <th class="px-4 py-3 text-center">التاريخ</th>
                                        <th class="px-4 py-3 text-center">العميل</th>
                                        <th class="px-4 py-3 text-center">الموظف</th>
                                        <th class="px-4 py-3 text-center">الحالة</th>
                                        <th class="px-4 py-3 text-center">عرض</th>
                                    </tr>
                                </thead>
                                <tbody id="reports-table-body" class="divide-y divide-gray-100 dark:divide-gray-700">
                                    <tr><td colspan="7" class="text-center py-8 text-gray-500">لا توجد بيانات</tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </main>
        </div>
    `;
    
    document.body.insertAdjacentHTML('beforeend', reportsHTML);
}

function closePermanentReportsPage() {
    const reportsPage = document.getElementById('reports-page');
    if (reportsPage) reportsPage.classList.add('hidden');
    
    const adminPage = document.getElementById('admin-page');
    if (adminPage) adminPage.classList.remove('hidden');
}

function getAllPermanentReportItems() {
    let items = [];
    
    (appCache.data.sales || []).forEach(item => {
        items.push({
            type: 'أمر بيع',
            id: getSafeValue(item, 'معرف'),
            date: getSafeValue(item, 'التاريخ'),
            client: getSafeValue(item, 'العميل'),
            employee: getSafeValue(item, 'الموظف'),
            status: getSafeValue(item, 'الحالة') || 'قيد الاعتماد',
            rawData: item
        });
    });
    
    (appCache.data.quotes || []).forEach(item => {
        items.push({
            type: 'عرض سعر',
            id: getSafeValue(item, 'معرف'),
            date: getSafeValue(item, 'التاريخ'),
            client: getSafeValue(item, 'العميل'),
            employee: getSafeValue(item, 'الموظف'),
            status: getSafeValue(item, 'الحالة') || 'قيد الاعتماد',
            rawData: item
        });
    });
    
    (appCache.data.complaints || []).forEach(item => {
        items.push({
            type: 'شكوى',
            id: getSafeValue(item, 'معرف'),
            date: getSafeValue(item, 'التاريخ'),
            client: getSafeValue(item, 'العميل'),
            employee: getSafeValue(item, 'الموظف'),
            status: getSafeValue(item, 'الحالة') || 'قيد الاعتماد',
            rawData: item
        });
    });
    
    (appCache.data.customers || []).forEach(item => {
        items.push({
            type: 'عميل',
            id: getSafeValue(item, 'معرف'),
            date: getSafeValue(item, 'التاريخ'),
            client: getSafeValue(item, 'اسم_العميل') || getSafeValue(item, 'اسم العميل'),
            employee: getSafeValue(item, 'الموظف'),
            status: getSafeValue(item, 'الحالة') || 'قيد الاعتماد',
            rawData: item
        });
    });
    
    items.sort((a, b) => new Date(b.date) - new Date(a.date));
    return items;
}

function applyPermanentReportsFilter() {
    const typeFilter = document.getElementById('report-filter-type')?.value || 'all';
    const statusFilter = document.getElementById('report-filter-status')?.value || 'all';
    const fromDate = document.getElementById('report-filter-date-from')?.value;
    const toDate = document.getElementById('report-filter-date-to')?.value;
    
    let allItems = getAllPermanentReportItems();
    
    let filtered = allItems.filter(item => {
        if (typeFilter !== 'all' && item.type !== typeFilter) return false;
        if (statusFilter !== 'all' && item.status !== statusFilter) return false;
        if (fromDate && item.date && new Date(item.date) < new Date(fromDate)) return false;
        if (toDate && item.date && new Date(item.date) > new Date(toDate)) return false;
        return true;
    });
    
    renderPermanentReportsTable(filtered);
    updatePermanentReportSummary(filtered);
}

function renderPermanentReportsTable(items) {
    const tbody = document.getElementById('reports-table-body');
    if (!tbody) return;
    
    if (items.length === 0) {
        tbody.innerHTML = '<tr><td colspan="7" class="text-center py-12 text-gray-500">لا توجد بيانات</tr>';
        return;
    }
    
    tbody.innerHTML = items.map((item) => {
        let statusClass = '';
        if (item.status === 'معتمد') statusClass = 'badge-approved';
        else if (item.status === 'مرفوض') statusClass = 'badge-rejected';
        else statusClass = 'badge-pending';
        
        let docType = '';
        if (item.type === 'أمر بيع') docType = 'sale';
        else if (item.type === 'عرض سعر') docType = 'quote';
        else if (item.type === 'شكوى') docType = 'complaint';
        else if (item.type === 'عميل') docType = 'customer';
        else docType = 'sale';
        
        return `
            <tr class="hover:bg-gray-50 transition-colors border-b border-gray-100">
                <td class="px-4 py-3 text-center">${item.type}</td>
                <td class="px-4 py-3 text-center">${item.id || '-'}</td>
                <td class="px-4 py-3 text-center">${formatDate(item.date)}</td>
                <td class="px-4 py-3 text-center">${item.client || '-'}</td>
                <td class="px-4 py-3 text-center">${item.employee || '-'}</td>
                <td class="px-4 py-3 text-center"><span class="badge ${statusClass}">${item.status}</span></td>
                <td class="px-4 py-3 text-center">
                    <button onclick='showDocumentPreview(${JSON.stringify(item.rawData).replace(/'/g, "&apos;")}, "${docType}")' 
                            class="text-amber-500 hover:text-amber-600 p-2 rounded-lg hover:bg-amber-50">
                        <i class="ri-eye-line text-xl"></i>
                    </button>
                </td>
            </tr>
        `;
    }).join('');
}

function updatePermanentReportSummary(items) {
    const summaryEl = document.getElementById('report-summary');
    if (!summaryEl) return;
    
    const total = items.length;
    const approved = items.filter(i => i.status === 'معتمد').length;
    const pending = items.filter(i => i.status === 'قيد الاعتماد').length;
    const rejected = items.filter(i => i.status === 'مرفوض').length;
    
    summaryEl.innerHTML = `
        <div class="flex flex-wrap gap-4 p-4 bg-gray-50 dark:bg-gray-800 rounded-xl">
            <div class="flex items-center gap-2"><div class="w-3 h-3 rounded-full bg-primary"></div><span>الإجمالي: ${total}</span></div>
            <div class="flex items-center gap-2"><div class="w-3 h-3 rounded-full bg-green-500"></div><span>معتمد: ${approved}</span></div>
            <div class="flex items-center gap-2"><div class="w-3 h-3 rounded-full bg-yellow-500"></div><span>قيد الاعتماد: ${pending}</span></div>
            <div class="flex items-center gap-2"><div class="w-3 h-3 rounded-full bg-red-500"></div><span>مرفوض: ${rejected}</span></div>
        </div>
    `;
}

function resetPermanentReportsFilter() {
    const typeSelect = document.getElementById('report-filter-type');
    const statusSelect = document.getElementById('report-filter-status');
    const fromDate = document.getElementById('report-filter-date-from');
    const toDate = document.getElementById('report-filter-date-to');
    
    if (typeSelect) typeSelect.value = 'all';
    if (statusSelect) statusSelect.value = 'all';
    if (fromDate) fromDate.value = '';
    if (toDate) toDate.value = '';
    
    applyPermanentReportsFilter();
}

function exportPermanentReportsToExcel() {
    const items = getAllPermanentReportItems();
    
    if (items.length === 0) {
        alert('لا توجد بيانات للتصدير');
        return;
    }
    
    const exportData = items.map(item => ({
        'النوع': item.type,
        'رقم المستند': item.id,
        'التاريخ': formatDate(item.date),
        'العميل': item.client || '-',
        'الموظف': item.employee || '-',
        'الحالة': item.status
    }));
    
    const ws = XLSX.utils.json_to_sheet(exportData);
    const wb = XLSX.utils.book_new();
    XLSX.utils.book_append_sheet(wb, ws, 'التقارير');
    XLSX.writeFile(wb, `تقرير_${new Date().toISOString().slice(0, 19).replace(/:/g, '-')}.xlsx`);
    
    alert('تم تصدير التقرير بنجاح');
}

function openEmailModalFromAdmin() {
    alert('📧 سيتم إضافة نافذة إرسال الإيميل قريباً');
    // يمكنك إضافة مودال الإيميل هنا لاحقاً
}

console.log('✅ تم تثبيت التعديلات بشكل دائم في النظام');

// ============================================
// نظام إرسال الإيميلات المتقدم - نسخة مصححة
// ============================================

// متغيرات عامة
let selectedEmails = [];

// ============================================
// فتح نافذة إرسال الإيميل
// ============================================

function openEmailModalFromAdmin() {
    // إزالة المودال القديم إذا وجد
    const oldModal = document.getElementById('advanced-email-modal');
    if (oldModal) {
        oldModal.remove();
    }
    
    // إنشاء المودال الجديد
    createAdvancedEmailModal();
    
    const modal = document.getElementById('advanced-email-modal');
    if (modal) {
        modal.classList.remove('hidden');
        loadEmailDocuments();
        
        // تعبئة البريد الإلكتروني تلقائياً من المستخدم الحالي
        const emailInput = document.getElementById('email-recipient');
        if (emailInput && currentUser && currentUser.email) {
            emailInput.value = currentUser.email;
        }
        
        // تعبئة عنوان الرسالة تلقائياً
        const subjectInput = document.getElementById('email-subject');
        if (subjectInput) {
            subjectInput.value = `مستندات من Hyma Plastic - ${new Date().toLocaleDateString('ar-EG')}`;
        }
    }
}

// ============================================
// إنشاء نافذة الإيميل المتقدمة
// ============================================

function createAdvancedEmailModal() {
    const modalHTML = `
        <div id="advanced-email-modal" class="fixed inset-0 flex items-center justify-center z-50 modal-backdrop" style="background: rgba(0,0,0,0.5); backdrop-filter: blur(4px);">
            <div class="bg-white dark:bg-gray-800 rounded-2xl p-6 w-full max-w-6xl mx-4 max-h-[90vh] overflow-y-auto shadow-2xl border border-gray-100 dark:border-gray-700">
                <div class="flex justify-between items-center mb-6 pb-4 border-b border-gray-100 dark:border-gray-700 sticky top-0 bg-white dark:bg-gray-800 z-10">
                    <h3 class="text-xl font-bold text-gray-800 dark:text-white flex items-center gap-2">
                        <i class="ri-mail-send-line text-primary"></i>
                        إرسال مستندات عبر البريد الإلكتروني
                    </h3>
                    <button onclick="closeAdvancedEmailModal()" class="text-gray-400 hover:text-gray-600 transition-colors p-2 hover:bg-gray-100 rounded-lg">
                        <i class="ri-close-line text-2xl"></i>
                    </button>
                </div>
                
                <!-- نموذج البريد الإلكتروني -->
                <div class="bg-gray-50 dark:bg-gray-900/50 rounded-xl p-4 mb-6">
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-sm font-bold text-gray-700 dark:text-gray-300 mb-2">
                                <i class="ri-mail-line text-primary ml-1"></i> البريد الإلكتروني للمستلم <span class="text-red-500">*</span>
                            </label>
                            <input type="email" id="email-recipient" 
                                   class="w-full px-4 py-2.5 border-2 border-gray-200 dark:border-gray-700 dark:bg-gray-900 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all"
                                   placeholder="example@company.com">
                            <p class="text-xs text-gray-400 mt-1">سيتم إرسال المستندات إلى هذا البريد</p>
                        </div>
                        <div>
                            <label class="block text-sm font-bold text-gray-700 dark:text-gray-300 mb-2">
                                <i class="ri-mail-send-line text-primary ml-1"></i> البريد الإلكتروني CC (اختياري)
                            </label>
                            <input type="email" id="email-cc" 
                                   class="w-full px-4 py-2.5 border-2 border-gray-200 dark:border-gray-700 dark:bg-gray-900 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all"
                                   placeholder="cc@company.com">
                        </div>
                    </div>
                    <div class="mt-4">
                        <label class="block text-sm font-bold text-gray-700 dark:text-gray-300 mb-2">
                            <i class="ri-heading-line text-primary ml-1"></i> عنوان الرسالة
                        </label>
                        <input type="text" id="email-subject" 
                               class="w-full px-4 py-2.5 border-2 border-gray-200 dark:border-gray-700 dark:bg-gray-900 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all"
                               placeholder="عنوان البريد الإلكتروني">
                    </div>
                    <div class="mt-4">
                        <label class="block text-sm font-bold text-gray-700 dark:text-gray-300 mb-2">
                            <i class="ri-chat-1-line text-primary ml-1"></i> نص الرسالة
                        </label>
                        <textarea id="email-body" rows="3" 
                                  class="w-full px-4 py-2.5 border-2 border-gray-200 dark:border-gray-700 dark:bg-gray-900 rounded-xl focus:border-primary focus:ring-4 focus:ring-primary/10 transition-all resize-none"
                                  placeholder="نص الرسالة الإضافي..."></textarea>
                    </div>
                </div>
                
                <!-- قسم الفلاتر -->
                <div class="mb-6">
                    <h4 class="text-lg font-bold text-gray-800 dark:text-white mb-3 flex items-center gap-2">
                        <i class="ri-filter-3-line text-primary"></i>
                        فلترة المستندات
                    </h4>
                    <div class="grid grid-cols-1 md:grid-cols-4 gap-4 bg-gray-50 dark:bg-gray-900/50 rounded-xl p-4">
                        <div>
                            <label class="block text-sm font-bold text-gray-700 dark:text-gray-300 mb-1">الموظف</label>
                            <select id="filter-employee" onchange="filterEmailDocuments()" 
                                    class="w-full px-3 py-2 border border-gray-200 dark:border-gray-700 dark:bg-gray-900 rounded-lg">
                                <option value="all">جميع الموظفين</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-sm font-bold text-gray-700 dark:text-gray-300 mb-1">نوع المستند</label>
                            <select id="filter-doc-type" onchange="filterEmailDocuments()" 
                                    class="w-full px-3 py-2 border border-gray-200 dark:border-gray-700 dark:bg-gray-900 rounded-lg">
                                <option value="all">الكل</option>
                                <option value="sale">أوامر البيع</option>
                                <option value="quote">عروض الأسعار</option>
                                <option value="complaint">الشكاوى</option>
                                <option value="customer">العملاء</option>
                                <option value="visit">الزيارات</option>
                                <option value="activity">الأنشطة اليومية</option>
                                <option value="plan">الخطط الأسبوعية</option>
                                <option value="collection">التحصيلات</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-sm font-bold text-gray-700 dark:text-gray-300 mb-1">من تاريخ</label>
                            <input type="date" id="filter-date-from" onchange="filterEmailDocuments()" 
                                   class="w-full px-3 py-2 border border-gray-200 dark:border-gray-700 dark:bg-gray-900 rounded-lg">
                        </div>
                        <div>
                            <label class="block text-sm font-bold text-gray-700 dark:text-gray-300 mb-1">إلى تاريخ</label>
                            <input type="date" id="filter-date-to" onchange="filterEmailDocuments()" 
                                   class="w-full px-3 py-2 border border-gray-200 dark:border-gray-700 dark:bg-gray-900 rounded-lg">
                        </div>
                    </div>
                </div>
                
                <!-- أزرار التحكم في الاختيار -->
                <div class="flex justify-between items-center mb-4">
                    <div class="flex gap-3">
                        <button type="button" onclick="selectAllDocuments()" 
                                class="bg-primary/10 hover:bg-primary/20 text-primary px-4 py-2 rounded-lg text-sm font-medium transition-all flex items-center gap-2">
                            <i class="ri-checkbox-line"></i> تحديد الكل
                        </button>
                        <button type="button" onclick="deselectAllDocuments()" 
                                class="bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 text-gray-700 dark:text-gray-300 px-4 py-2 rounded-lg text-sm font-medium transition-all flex items-center gap-2">
                            <i class="ri-checkbox-blank-line"></i> إلغاء الكل
                        </button>
                    </div>
                    <div class="text-sm text-gray-500">
                        المختار: <span id="selected-count">0</span> مستند
                    </div>
                </div>
                
                <!-- قائمة المستندات -->
                <div class="border border-gray-200 dark:border-gray-700 rounded-xl overflow-hidden mb-6">
                    <div class="bg-gray-50 dark:bg-gray-900/50 px-4 py-3 border-b border-gray-200 dark:border-gray-700 flex items-center gap-4">
                        <div class="w-8 text-center">
                            <input type="checkbox" id="select-all-checkbox" onchange="toggleSelectAll()" class="w-4 h-4">
                        </div>
                        <div class="flex-1 grid grid-cols-12 gap-2 text-sm font-bold text-gray-700 dark:text-gray-300">
                            <div class="col-span-2">نوع المستند</div>
                            <div class="col-span-2">رقم المستند</div>
                            <div class="col-span-2">التاريخ</div>
                            <div class="col-span-2">الموظف</div>
                            <div class="col-span-3">العميل</div>
                            <div class="col-span-1">عرض</div>
                        </div>
                    </div>
                    <div id="documents-list-container" class="max-h-96 overflow-y-auto divide-y divide-gray-100 dark:divide-gray-700">
                        <div class="text-center py-8 text-gray-500">جاري تحميل المستندات...</div>
                    </div>
                </div>
                
                <!-- أزرار الإرسال -->
                <div class="flex gap-3 pt-4 border-t border-gray-100 dark:border-gray-700">
                    <button type="button" onclick="sendSelectedDocuments()" 
                            class="flex-1 bg-gradient-to-r from-primary to-primaryDark text-white py-3.5 rounded-xl font-bold shadow-lg shadow-primary/30 hover:shadow-xl transition-all duration-300 flex items-center justify-center gap-2">
                        <i class="ri-send-plane-line text-lg"></i>
                        <span>إرسال المستندات المختارة</span>
                    </button>
                    <button type="button" onclick="closeAdvancedEmailModal()" 
                            class="flex-1 bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 text-gray-700 dark:text-gray-300 py-3.5 rounded-xl font-bold transition-all duration-300 flex items-center justify-center gap-2">
                        <i class="ri-close-line text-lg"></i>
                        <span>إلغاء</span>
                    </button>
                </div>
            </div>
        </div>
    `;
    
    document.body.insertAdjacentHTML('beforeend', modalHTML);
}

// ============================================
// إرسال المستندات المختارة (نسخة مصححة)
// ============================================

async function sendSelectedDocuments() {
    // الحصول على البريد الإلكتروني
    const recipientInput = document.getElementById('email-recipient');
    const recipient = recipientInput?.value?.trim();
    
    // التحقق من وجود البريد الإلكتروني
    if (!recipient) {
        showEmailError('يرجى إدخال البريد الإلكتروني للمستلم');
        if (recipientInput) recipientInput.focus();
        return;
    }
    
    // التحقق من صحة البريد الإلكتروني
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailRegex.test(recipient)) {
        showEmailError('البريد الإلكتروني غير صحيح. مثال: name@company.com');
        if (recipientInput) recipientInput.focus();
        return;
    }
    
    // التحقق من وجود مستندات مختارة
    if (!selectedEmails || selectedEmails.length === 0) {
        showEmailError('يرجى اختيار مستند واحد على الأقل للإرسال');
        return;
    }
    
    // جمع البيانات
    const subject = document.getElementById('email-subject')?.value || `مستندات من Hyma Plastic - ${new Date().toLocaleDateString('ar-EG')}`;
    const body = document.getElementById('email-body')?.value || `تم إرفاق ${selectedEmails.length} مستند(مستندات) من نظام Hyma Plastic`;
    const cc = document.getElementById('email-cc')?.value || '';
    
    // تجميع المستندات المختارة
    const selectedDocs = [];
    for (const selectedId of selectedEmails) {
        const [type, id] = selectedId.split('_');
        let doc = null;
        
        switch(type) {
            case 'sale':
                doc = appCache.data.sales?.find(d => getSafeValue(d, 'معرف') == id);
                break;
            case 'quote':
                doc = appCache.data.quotes?.find(d => getSafeValue(d, 'معرف') == id);
                break;
            case 'complaint':
                doc = appCache.data.complaints?.find(d => getSafeValue(d, 'معرف') == id);
                break;
            case 'customer':
                doc = appCache.data.customers?.find(d => getSafeValue(d, 'معرف') == id);
                break;
            case 'visit':
                doc = appCache.data.visits?.find(d => getSafeValue(d, 'معرف') == id);
                break;
            case 'activity':
                doc = appCache.data.activities?.find(d => getSafeValue(d, 'معرف') == id);
                break;
            case 'plan':
                doc = appCache.data.plans?.find(d => getSafeValue(d, 'معرف') == id);
                break;
            case 'collection':
                doc = appCache.data.collections?.find(d => getSafeValue(d, 'معرف') == id);
                break;
        }
        
        if (doc) {
            selectedDocs.push({ type, id, data: doc });
        }
    }
    
    if (selectedDocs.length === 0) {
        showEmailError('لم يتم العثور على المستندات المختارة');
        return;
    }
    
    // تعطيل زر الإرسال أثناء العملية
    const sendBtn = document.querySelector('#advanced-email-modal button[onclick="sendSelectedDocuments()"]');
    const originalText = sendBtn?.innerHTML;
    if (sendBtn) {
        sendBtn.innerHTML = '<i class="ri-loader-4-line animate-spin text-lg"></i><span> جاري الإرسال...</span>';
        sendBtn.disabled = true;
    }
    
    try {
        const res = await sendRequest({
            action: 'SEND_EMAIL_WITH_DOCS',
            recipient: recipient,
            cc: cc,
            subject: subject,
            body: body,
            documents: JSON.stringify(selectedDocs.map(doc => ({
                type: doc.type,
                id: doc.id,
                data: doc.data
            })))
        });
        
        if (res.success) {
            showEmailSuccess(`✅ تم إرسال ${selectedDocs.length} مستند بنجاح إلى ${recipient}`);
            setTimeout(() => closeAdvancedEmailModal(), 2000);
        } else {
            showEmailError(res.error || 'فشل إرسال البريد الإلكتروني');
        }
    } catch (err) {
        console.error('Error:', err);
        showEmailError('خطأ في الاتصال: ' + err.message);
    } finally {
        if (sendBtn) {
            sendBtn.innerHTML = originalText;
            sendBtn.disabled = false;
        }
    }
}


// ============================================
// منع ظهور أزرار الرسائل وقائمة الأسعار للمدير
// ============================================

(function hideAdminButtonsFromManager() {
    
    function hideButtons() {
        // التأكد من وجود المستخدم
        if (!currentUser) {
            setTimeout(hideButtons, 500);
            return;
        }
        
        // البحث عن أزرار الرسائل وقائمة الأسعار
        const messagesBtn = document.querySelector('#admin-page button[onclick="openMessagesModal()"]');
        const priceListBtn = document.querySelector('#admin-page button[onclick="openPriceListModal()"]');
        
        // إذا كان المستخدم مدير (Manager)
        if (currentUser.role === 'manager') {
            // إخفاء زر الرسائل
            if (messagesBtn) {
                messagesBtn.style.display = 'none';
                messagesBtn.remove(); // إزالة الزر بالكامل
                console.log('✅ تم إخفاء زر الرسائل للمدير');
            }
            
            // إخفاء زر قائمة الأسعار
            if (priceListBtn) {
                priceListBtn.style.display = 'none';
                priceListBtn.remove(); // إزالة الزر بالكامل
                console.log('✅ تم إخفاء زر قائمة الأسعار للمدير');
            }
        }
        
        // إذا كان المستخدم مسؤول (Admin)
        if (currentUser.role === 'admin') {
            // التأكد من ظهور الأزرار
            if (messagesBtn) {
                messagesBtn.style.display = 'inline-flex';
            }
            if (priceListBtn) {
                priceListBtn.style.display = 'inline-flex';
            }
            console.log('✅ أزرار الرسائل وقائمة الأسعار ظاهرة للمسؤول');
        }
    }
    
    // تنفيذ فوراً
    if (document.readyState === 'loading') {
        document.addEventListener('DOMContentLoaded', hideButtons);
    } else {
        hideButtons();
    }
    
    // مراقبة التغييرات في الصفحة (للتأكد من عدم ظهور الأزرار مرة أخرى)
    const observer = new MutationObserver(function(mutations) {
        hideButtons();
    });
    
    // بدء المراقبة بعد تحميل الصفحة
    setTimeout(() => {
        const adminPage = document.getElementById('admin-page');
        if (adminPage) {
            observer.observe(adminPage, { childList: true, subtree: true });
        }
    }, 1000);
    
})();

// ============================================
// أيضاً منع الوصول للدوال إذا كان المستخدم مدير
// ============================================

// حفظ الدوال الأصلية
const originalOpenMessagesModal = window.openMessagesModal;
const originalOpenPriceListModal = window.openPriceListModal;

// استبدال الدوال بحماية
window.openMessagesModal = function() {
    if (currentUser && currentUser.role === 'admin') {
        if (originalOpenMessagesModal) {
            originalOpenMessagesModal();
        }
    } else {
        console.warn('⚠️ ليس لديك صلاحية للوصول إلى الرسائل');
        showToastForManager('هذه الميزة متاحة للمسؤول فقط');
    }
};

window.openPriceListModal = function() {
    if (currentUser && currentUser.role === 'admin') {
        if (originalOpenPriceListModal) {
            originalOpenPriceListModal();
        }
    } else {
        console.warn('⚠️ ليس لديك صلاحية للوصول إلى قائمة الأسعار');
        showToastForManager('هذه الميزة متاحة للمسؤول فقط');
    }
};

// دالة عرض رسالة للمدير
function showToastForManager(message) {
    const toast = document.createElement('div');
    toast.className = 'fixed top-20 left-1/2 transform -translate-x-1/2 z-50 flex items-center gap-3 px-6 py-3 rounded-xl shadow-lg bg-red-500 text-white animate-slide-up';
    toast.innerHTML = `<i class="ri-close-circle-line text-xl"></i><span>${message}</span>`;
    document.body.appendChild(toast);
    setTimeout(() => toast.remove(), 3000);
}

console.log('✅ تم تفعيل نظام الصلاحيات:');
console.log('   - المسؤول (admin): يظهر له جميع الأزرار');
console.log('   - المدير (manager): لا يظهر له أزرار الرسائل وقائمة الأسعار');
// ============================================
// دوال عرض الرسائل
// ============================================

function showEmailError(message) {
    // إزالة أي رسالة خطأ سابقة
    const existingError = document.querySelector('.email-error-toast');
    if (existingError) existingError.remove();
    
    const toast = document.createElement('div');
    toast.className = 'email-error-toast fixed top-20 left-1/2 transform -translate-x-1/2 z-50 flex items-center gap-3 px-6 py-3 rounded-xl shadow-lg bg-red-500 text-white animate-slide-up';
    toast.innerHTML = `<i class="ri-close-circle-line text-xl"></i><span>${message}</span>`;
    document.body.appendChild(toast);
    
    // تمييز حقل البريد باللون الأحمر
    const emailInput = document.getElementById('email-recipient');
    if (emailInput) {
        emailInput.classList.add('border-red-500', 'bg-red-50');
        setTimeout(() => {
            emailInput.classList.remove('border-red-500', 'bg-red-50');
        }, 3000);
    }
    
    setTimeout(() => toast.remove(), 4000);
}

function showEmailSuccess(message) {
    const toast = document.createElement('div');
    toast.className = 'fixed top-20 left-1/2 transform -translate-x-1/2 z-50 flex items-center gap-3 px-6 py-3 rounded-xl shadow-lg bg-green-500 text-white animate-slide-up';
    toast.innerHTML = `<i class="ri-check-line text-xl"></i><span>${message}</span>`;
    document.body.appendChild(toast);
    setTimeout(() => toast.remove(), 3000);
}

// ============================================
// باقي الدوال المساعدة (نفس ما كانت)
// ============================================

function loadEmailDocuments() {
    const employeeFilter = document.getElementById('filter-employee');
    if (employeeFilter) {
        const employees = new Set();
        const allDocs = getAllDocumentsForEmail();
        allDocs.forEach(doc => {
            if (doc.employee && doc.employee !== '') {
                employees.add(doc.employee);
            }
        });
        
        employeeFilter.innerHTML = '<option value="all">جميع الموظفين</option>' + 
            Array.from(employees).sort().map(emp => `<option value="${emp}">${emp}</option>`).join('');
    }
    
    filterEmailDocuments();
}

function getAllDocumentsForEmail() {
    let allDocs = [];
    
    (appCache.data.sales || []).forEach(item => {
        allDocs.push({
            type: 'sale',
            typeName: 'أمر بيع',
            id: getSafeValue(item, 'معرف'),
            date: getSafeValue(item, 'التاريخ'),
            employee: getSafeValue(item, 'الموظف'),
            client: getSafeValue(item, 'العميل'),
            status: getSafeValue(item, 'الحالة'),
            rawData: item
        });
    });
    
    (appCache.data.quotes || []).forEach(item => {
        allDocs.push({
            type: 'quote',
            typeName: 'عرض سعر',
            id: getSafeValue(item, 'معرف'),
            date: getSafeValue(item, 'التاريخ'),
            employee: getSafeValue(item, 'الموظف'),
            client: getSafeValue(item, 'العميل'),
            status: getSafeValue(item, 'الحالة'),
            rawData: item
        });
    });
    
    (appCache.data.complaints || []).forEach(item => {
        allDocs.push({
            type: 'complaint',
            typeName: 'شكوى',
            id: getSafeValue(item, 'معرف'),
            date: getSafeValue(item, 'التاريخ'),
            employee: getSafeValue(item, 'الموظف'),
            client: getSafeValue(item, 'العميل'),
            status: getSafeValue(item, 'الحالة'),
            rawData: item
        });
    });
    
    (appCache.data.customers || []).forEach(item => {
        allDocs.push({
            type: 'customer',
            typeName: 'عميل',
            id: getSafeValue(item, 'معرف'),
            date: getSafeValue(item, 'التاريخ'),
            employee: getSafeValue(item, 'الموظف'),
            client: getSafeValue(item, 'اسم_العميل') || getSafeValue(item, 'اسم العميل'),
            status: getSafeValue(item, 'الحالة'),
            rawData: item
        });
    });
    
    (appCache.data.visits || []).forEach(item => {
        allDocs.push({
            type: 'visit',
            typeName: 'زيارة',
            id: getSafeValue(item, 'معرف'),
            date: getSafeValue(item, 'التاريخ'),
            employee: getSafeValue(item, 'الموظف'),
            client: getSafeValue(item, 'العميل'),
            status: 'مكتمل',
            rawData: item
        });
    });
    
    (appCache.data.activities || []).forEach(item => {
        allDocs.push({
            type: 'activity',
            typeName: 'نشاط يومي',
            id: getSafeValue(item, 'معرف'),
            date: getSafeValue(item, 'التاريخ'),
            employee: getSafeValue(item, 'الموظف'),
            client: '-',
            status: 'مكتمل',
            rawData: item
        });
    });
    
    (appCache.data.plans || []).forEach(item => {
        allDocs.push({
            type: 'plan',
            typeName: 'خطة أسبوعية',
            id: getSafeValue(item, 'معرف'),
            date: getSafeValue(item, 'من_تاريخ') || getSafeValue(item, 'من تاريخ'),
            employee: getSafeValue(item, 'الموظف'),
            client: '-',
            status: 'مخطط',
            rawData: item
        });
    });
    
    (appCache.data.collections || []).forEach(item => {
        allDocs.push({
            type: 'collection',
            typeName: 'تحصيل',
            id: getSafeValue(item, 'معرف'),
            date: getSafeValue(item, 'التاريخ'),
            employee: getSafeValue(item, 'الموظف'),
            client: getSafeValue(item, 'العميل'),
            status: getSafeValue(item, 'الحالة'),
            rawData: item
        });
    });
    
    allDocs.sort((a, b) => new Date(b.date) - new Date(a.date));
    return allDocs;
}

function filterEmailDocuments() {
    const employee = document.getElementById('filter-employee')?.value || 'all';
    const docType = document.getElementById('filter-doc-type')?.value || 'all';
    const dateFrom = document.getElementById('filter-date-from')?.value;
    const dateTo = document.getElementById('filter-date-to')?.value;
    
    let allDocs = getAllDocumentsForEmail();
    
    let filtered = allDocs.filter(doc => {
        if (employee !== 'all' && doc.employee !== employee) return false;
        if (docType !== 'all' && doc.type !== docType) return false;
        if (dateFrom && doc.date && new Date(doc.date) < new Date(dateFrom)) return false;
        if (dateTo && doc.date && new Date(doc.date) > new Date(dateTo)) return false;
        return true;
    });
    
    renderDocumentsList(filtered);
}

function renderDocumentsList(documents) {
    const container = document.getElementById('documents-list-container');
    if (!container) return;
    
    if (documents.length === 0) {
        container.innerHTML = '<div class="text-center py-12 text-gray-500">لا توجد مستندات تطابق معايير البحث</div>';
        document.getElementById('selected-count').innerText = '0';
        return;
    }
    
    selectedEmails = [];
    
    container.innerHTML = documents.map((doc, index) => {
        const docId = `${doc.type}_${doc.id}`;
        return `
            <div class="flex items-center gap-4 px-4 py-3 hover:bg-gray-50 dark:hover:bg-gray-800 transition-colors">
                <div class="w-8 text-center">
                    <input type="checkbox" class="doc-checkbox" data-id="${docId}" onchange="toggleDocumentSelection(this, '${docId}')">
                </div>
                <div class="flex-1 grid grid-cols-12 gap-2 text-sm">
                    <div class="col-span-2">
                        <span class="inline-flex items-center gap-1 px-2 py-1 rounded-full text-xs font-medium ${getTypeColor(doc.type)}">
                            <i class="ri-${getTypeIcon(doc.type)} text-xs"></i>
                            ${doc.typeName}
                        </span>
                    </div>
                    <div class="col-span-2 font-mono text-xs">${doc.id || '-'}</div>
                    <div class="col-span-2">${formatDate(doc.date)}</div>
                    <div class="col-span-2 font-medium">${doc.employee || '-'}</div>
                    <div class="col-span-3 truncate" title="${doc.client}">${doc.client || '-'}</div>
                    <div class="col-span-1">
                        <button onclick="previewEmailDocument('${doc.type}', '${doc.id}')" 
                                class="text-amber-500 hover:text-amber-600 p-1 rounded hover:bg-amber-50">
                            <i class="ri-eye-line text-lg"></i>
                        </button>
                    </div>
                </div>
            </div>
        `;
    }).join('');
    
    updateSelectedCount();
}

function getTypeColor(type) {
    const colors = {
        'sale': 'bg-blue-100 text-blue-700',
        'quote': 'bg-green-100 text-green-700',
        'complaint': 'bg-red-100 text-red-700',
        'customer': 'bg-purple-100 text-purple-700',
        'visit': 'bg-indigo-100 text-indigo-700',
        'activity': 'bg-teal-100 text-teal-700',
        'plan': 'bg-cyan-100 text-cyan-700',
        'collection': 'bg-amber-100 text-amber-700'
    };
    return colors[type] || 'bg-gray-100 text-gray-700';
}

function getTypeIcon(type) {
    const icons = {
        'sale': 'shopping-cart-line',
        'quote': 'file-list-line',
        'complaint': 'alert-line',
        'customer': 'user-line',
        'visit': 'map-pin-line',
        'activity': 'calendar-check-line',
        'plan': 'calendar-todo-line',
        'collection': 'money-dollar-circle-line'
    };
    return icons[type] || 'file-line';
}

function toggleDocumentSelection(checkbox, docId) {
    if (checkbox.checked) {
        if (!selectedEmails.includes(docId)) {
            selectedEmails.push(docId);
        }
    } else {
        selectedEmails = selectedEmails.filter(id => id !== docId);
    }
    updateSelectedCount();
    updateSelectAllCheckbox();
}

function toggleSelectAll() {
    const selectAllCheckbox = document.getElementById('select-all-checkbox');
    const checkboxes = document.querySelectorAll('.doc-checkbox');
    
    checkboxes.forEach(cb => {
        cb.checked = selectAllCheckbox.checked;
        const docId = cb.getAttribute('data-id');
        if (selectAllCheckbox.checked) {
            if (!selectedEmails.includes(docId)) {
                selectedEmails.push(docId);
            }
        } else {
            selectedEmails = selectedEmails.filter(id => id !== docId);
        }
    });
    
    updateSelectedCount();
}

function selectAllDocuments() {
    const checkboxes = document.querySelectorAll('.doc-checkbox');
    checkboxes.forEach(cb => {
        cb.checked = true;
        const docId = cb.getAttribute('data-id');
        if (!selectedEmails.includes(docId)) {
            selectedEmails.push(docId);
        }
    });
    updateSelectedCount();
    updateSelectAllCheckbox();
}

function deselectAllDocuments() {
    const checkboxes = document.querySelectorAll('.doc-checkbox');
    checkboxes.forEach(cb => {
        cb.checked = false;
    });
    selectedEmails = [];
    updateSelectedCount();
    updateSelectAllCheckbox();
}

function updateSelectedCount() {
    const countSpan = document.getElementById('selected-count');
    if (countSpan) {
        countSpan.innerText = selectedEmails.length;
    }
}

function updateSelectAllCheckbox() {
    const selectAllCheckbox = document.getElementById('select-all-checkbox');
    const checkboxes = document.querySelectorAll('.doc-checkbox');
    if (selectAllCheckbox && checkboxes.length > 0) {
        const allChecked = Array.from(checkboxes).every(cb => cb.checked);
        selectAllCheckbox.checked = allChecked;
    }
}

function previewEmailDocument(type, id) {
    let doc = null;
    
    switch(type) {
        case 'sale':
            doc = appCache.data.sales?.find(d => getSafeValue(d, 'معرف') == id);
            break;
        case 'quote':
            doc = appCache.data.quotes?.find(d => getSafeValue(d, 'معرف') == id);
            break;
        case 'complaint':
            doc = appCache.data.complaints?.find(d => getSafeValue(d, 'معرف') == id);
            break;
        case 'customer':
            doc = appCache.data.customers?.find(d => getSafeValue(d, 'معرف') == id);
            break;
        case 'visit':
            doc = appCache.data.visits?.find(d => getSafeValue(d, 'معرف') == id);
            break;
        case 'activity':
            doc = appCache.data.activities?.find(d => getSafeValue(d, 'معرف') == id);
            break;
        case 'plan':
            doc = appCache.data.plans?.find(d => getSafeValue(d, 'معرف') == id);
            break;
        case 'collection':
            doc = appCache.data.collections?.find(d => getSafeValue(d, 'معرف') == id);
            break;
    }
    
    if (doc && typeof showDocumentPreview === 'function') {
        showDocumentPreview(doc, type);
    } else {
        showEmailError('لا يمكن عرض المستند حالياً');
    }
}

function closeAdvancedEmailModal() {
    const modal = document.getElementById('advanced-email-modal');
    if (modal) {
        modal.classList.add('hidden');
        setTimeout(() => modal.remove(), 300);
    }
    selectedEmails = [];
}

console.log('✅ تم تحديث نظام إرسال الإيميلات بنجاح');

// ═══════════════════════════════════════════════════════════════════════════
// القسم الحادي عشر: دوال التصدير والبريد الإلكتروني
// ═══════════════════════════════════════════════════════════════════════════

function openExportFilterModal(type) {
    const exportType = document.getElementById('export-type');
    const modal = document.getElementById('export-filter-modal');
    if (exportType) exportType.value = type;
    if (modal) modal.classList.remove('hidden');
}

function closeExportFilterModal() {
    const modal = document.getElementById('export-filter-modal');
    if (modal) modal.classList.add('hidden');
}

async function exportFilteredData(e) {
    e.preventDefault();
    const type = document.getElementById('export-type')?.value;
    const fromDate = document.getElementById('export-date-from')?.value;
    const toDate = document.getElementById('export-date-to')?.value;
    
    let data = [];
    let sheetName = '';
    
    switch(type) {
        case 'customers': data = appCache.data.customers; sheetName = 'العملاء'; break;
        case 'sales': data = appCache.data.sales; sheetName = 'المبيعات'; break;
        case 'quotes': data = appCache.data.quotes; sheetName = 'عروض الأسعار'; break;
        case 'complaints': data = appCache.data.complaints; sheetName = 'الشكاوى'; break;
        case 'visits': data = appCache.data.visits; sheetName = 'الزيارات'; break;
        case 'activities': data = appCache.data.activities; sheetName = 'الأنشطة'; break;
        case 'plans': data = appCache.data.plans; sheetName = 'الخطط'; break;
        case 'collections': data = appCache.data.collections; sheetName = 'التحصيلات'; break;
    }
    
    if (fromDate && toDate) {
        data = data.filter(item => {
            const itemDate = getSafeValue(item, 'التاريخ');
            if (!itemDate) return false;
            const dateOnly = itemDate.split(' ')[0];
            return dateOnly >= fromDate && dateOnly <= toDate;
        });
    }
    
    const res = await sendRequest({
        action: 'EXPORT_EXCEL',
        sheetName: sheetName,
        data: JSON.stringify(data)
    });
    
    if (res.success && res.data) {
        const link = document.createElement('a');
        link.href = res.data;
        link.download = `${sheetName}_${new Date().toISOString().split('T')[0]}.xlsx`;
        link.click();
        showSuccess('تم التصدير بنجاح');
        closeExportFilterModal();
    } else {
        showError(res.error || 'فشل التصدير');
    }
}

function openEmailModal(type, id) {
    let ids = [];
    if (id) {
        ids = [id];
    } else {
        let checkboxes;
        if (type === 'sale') checkboxes = document.querySelectorAll('.sale-checkbox:checked');
        else if (type === 'quote') checkboxes = document.querySelectorAll('.quote-checkbox:checked');
        else if (type === 'complaint') checkboxes = document.querySelectorAll('.complaint-checkbox:checked');
        ids = Array.from(checkboxes || []).map(cb => cb.value);
    }
    
    if (ids.length === 0) {
        showError('لم يتم تحديد أي مستند');
        return;
    }
    
    const emailType = document.getElementById('email-doc-type');
    const emailIds = document.getElementById('email-doc-ids');
    const modal = document.getElementById('email-send-modal');
    
    if (emailType) emailType.value = type;
    if (emailIds) emailIds.value = JSON.stringify(ids);
    if (modal) modal.classList.remove('hidden');
}

function closeEmailModal() {
    const modal = document.getElementById('email-send-modal');
    if (modal) modal.classList.add('hidden');
}

// ═══════════════════════════════════════════════════════════════════════════
// القسم الثاني عشر: دوال المرفقات والـ GPS
// ═══════════════════════════════════════════════════════════════════════════

function showAttachments(urls) {
    if (!urls || urls.trim() === '') {
        showError('لا توجد مرفقات');
        return;
    }
    const urlArray = urls.split(',').map(u => u.trim()).filter(u => u !== '');
    if (urlArray.length === 0) {
        showError('لا توجد مرفقات صالحة');
        return;
    }
    const list = document.getElementById('attachments-list');
    if (!list) return;
    
    list.innerHTML = '';
    const fragment = document.createDocumentFragment();
    
    urlArray.forEach(url => {
        const div = document.createElement('div');
        div.className = 'flex items-center gap-3 p-3 bg-gray-50 rounded-lg';
        div.innerHTML = `
            <i class="ri-file-line text-2xl text-primary"></i>
            <a href="${url}" target="_blank" class="text-primary hover:underline flex-1">${url.split('/').pop() || 'فتح المرفق'}</a>
        `;
        fragment.appendChild(div);
    });
    
    list.appendChild(fragment);
    const modal = document.getElementById('attachments-modal');
    if (modal) modal.classList.remove('hidden');
}

function getLocation() {
    if (!navigator.geolocation) {
        showError('المتصفح لا يدعم تحديد الموقع');
        return;
    }
    
    navigator.geolocation.getCurrentPosition(
        position => {
            const lat = position.coords.latitude;
            const lng = position.coords.longitude;
            const locField = document.getElementById('visit-location');
            if (locField) locField.value = `${lat}, ${lng}`;
        },
        error => {
            showError('فشل تحديد الموقع: ' + error.message);
        }
    );
}

// ═══════════════════════════════════════════════════════════════════════════
// القسم الثالث عشر: دوال تحميل البيانات وتحديث الواجهة (محسنة بالكامل)
// ═══════════════════════════════════════════════════════════════════════════

async function loadAllData(forceRefresh = false) {
    console.log('🔄 تحميل البيانات... forceRefresh:', forceRefresh);

    
    if (!forceRefresh && Date.now() - appCache.timestamp < appCache.CACHE_DURATION) {
        updateAllTables();
        return;
    }
    
    try {
        console.log('🌐 جلب البيانات من السيرفر...');
        
        const requests = [
            { name: 'sales', sheet: SHEET_CONFIG.SALES_SHEET_NAME },
            { name: 'complaints', sheet: SHEET_CONFIG.COMPLAINTS_SHEET_NAME },
            { name: 'quotes', sheet: SHEET_CONFIG.QUOTES_SHEET_NAME },
            { name: 'users', sheet: null, action: 'GET_USERS' },
            { name: 'customers', sheet: SHEET_CONFIG.CUSTOMERS_SHEET_NAME },
            { name: 'visits', sheet: SHEET_CONFIG.VISITS_SHEET_NAME },
            { name: 'activities', sheet: SHEET_CONFIG.ACTIVITIES_SHEET_NAME },
            { name: 'plans', sheet: SHEET_CONFIG.PLANS_SHEET_NAME },
            { name: 'collections', sheet: SHEET_CONFIG.COLLECTIONS_SHEET_NAME },
            { name: 'pendingUsers', sheet: null, action: 'GET_PENDING_USERS' },
            { name: 'items', sheet: SHEET_CONFIG.ITEMS_SHEET_NAME }
        ];

        const batchSize = 3;
        const results = [];
        
        for (let i = 0; i < requests.length; i += batchSize) {
            const batch = requests.slice(i, i + batchSize);
            const batchResults = await Promise.allSettled(
                batch.map(req => sendRequest({ 
                    action: req.action || 'GET', 
                    sheetName: req.sheet 
                }))
            );
            results.push(...batchResults);
        }

        results.forEach((result, index) => {
            const reqName = requests[index].name;
            if (result.status === 'fulfilled' && result.value.success) {
                appCache.set(reqName, result.value.data || []);
                console.log(`✅ ${reqName}: ${appCache.data[reqName].length} عنصر`);
            } else {
                console.error(`❌ فشل في تحميل ${reqName}:`, result.reason || result.value?.error);
                if (!appCache.data[reqName]) appCache.data[reqName] = [];
            }
        });

        updateSearchMaps();
        
        requestAnimationFrame(() => {
            updateAllTables();
            updateStats();
        });
        
        console.log('✅ تم تحميل جميع البيانات');
        return true;
        
    } catch (err) { 
        console.error('❌ خطأ في تحميل البيانات:', err); 
        return false; 
    }
}

function showLoading(show) {
    let loader = document.getElementById('global-loader');
    if (!loader && show) {
        loader = document.createElement('div');
        loader.id = 'global-loader';
        loader.className = 'fixed inset-0 bg-black/50 backdrop-blur-sm flex items-center justify-center z-[9999]';
        loader.innerHTML = `
            <div class="bg-white dark:bg-gray-800 rounded-2xl p-8 flex flex-col items-center gap-4 shadow-2xl">
                <div class="w-12 h-12 border-4 border-primary border-t-transparent rounded-full animate-spin"></div>
                <p class="text-gray-700 dark:text-gray-300 font-medium">جاري تحميل البيانات...</p>
            </div>
        `;
        document.body.appendChild(loader);
    } else if (loader && !show) {
        loader.remove();
    }
}

function updateAdminOnlyRow() {
    const adminRow = document.getElementById('admin-only-row');
    if (!adminRow) {
        console.warn('⚠️ عنصر admin-only-row غير موجود في الصفحة');
        return;
    }
    
    // تأكد من وجود currentUser
    if (!currentUser) {
        console.warn('⚠️ currentUser غير موجود');
        adminRow.classList.add('hidden');
        return;
    }
    
    // إظهار القسم إذا كان الدور admin
    if (currentUser.role === 'admin') {
        adminRow.classList.remove('hidden');
        console.log('✅ تم إظهار قسم الإدارة للمسؤول');
        
        // إعادة تحميل بيانات المستخدمين المعلقين للتأكد
        if (typeof loadAllData === 'function') {
            loadAllData(true);
        }
    } else {
        adminRow.classList.add('hidden');
        console.log('❌ تم إخفاء قسم الإدارة (الدور:', currentUser.role, ')');
    }
}

function showElementsByRole() {
    if (!currentUser) return;
    
    // عناصر تظهر فقط للمسؤول
    const adminOnlyElements = document.querySelectorAll('[data-role="admin"]');
    adminOnlyElements.forEach(el => {
        if (currentUser.role === 'admin') {
            el.classList.remove('hidden');
        } else {
            el.classList.add('hidden');
        }
    });
    
    // عناصر تظهر للمسؤول والمدير
    const adminManagerElements = document.querySelectorAll('[data-role="admin,manager"]');
    adminManagerElements.forEach(el => {
        if (currentUser.role === 'admin' || currentUser.role === 'manager') {
            el.classList.remove('hidden');
        } else {
            el.classList.add('hidden');
        }
    });
    
    // عناصر تظهر للجميع
    const allElements = document.querySelectorAll('[data-role="all"]');
    allElements.forEach(el => {
        el.classList.remove('hidden');
    });
}

function updateAllTables() {
    updateCustomersTable();
    updateSalesTable();
    updateQuotesTable();
    updateComplaintsTable();
    updateVisitsTable();
    updateActivitiesTable();
    updatePlansTable();
    updateCollectionsTable();
    updateUsersTable();
    updatePendingUsersTable();
    updateActivitiesLog();
    updateAdminOnlyRow();

}

function updateStats() {
    const stats = {
        'stats-total-customers': appCache.data.customers?.length || 0,
        'stats-total-plans': appCache.data.plans?.length || 0,
        'stats-total-visits': appCache.data.visits?.length || 0,
        'stats-total-activities': appCache.data.activities?.length || 0,
        'stats-total-quotes': appCache.data.quotes?.length || 0,
        'stats-total-sales': appCache.data.sales?.length || 0,
        'stats-total-complaints': appCache.data.complaints?.length || 0,
        'stats-total-collections': appCache.data.collections?.length || 0
    };
    
    requestAnimationFrame(() => {
        Object.entries(stats).forEach(([id, value]) => {
            const el = document.getElementById(id);
            if (el) el.textContent = value;
        });
    });
}

function updateCustomersTable() {
    const isAdminPage = document.getElementById('admin-page') && !document.getElementById('admin-page').classList.contains('hidden');
    const tableId = isAdminPage ? 'admin-customers-table' : 'my-customers-table';
    const table = document.getElementById(tableId);
    if (!table) return;
    
    const userCustomers = appCache.data.customers.filter(c => 
        currentUser.role === 'admin' || 
        currentUser.role === 'manager' ||
        usernameMatches(getSafeValue(c, 'الموظف'), currentUser.username)
    );
    
    console.log('📊 إجمالي العملاء المعروضين:', userCustomers.length);
    
    if (userCustomers.length === 0) {
        const cols = (currentUser.role === 'user') ? 12 : 13;
        table.innerHTML = `<tr><td colspan="${cols}" class="text-center py-8 text-gray-500">لا توجد بيانات</td></tr>`;
        return;
    }
    
    const fragment = document.createDocumentFragment();
    const isUser = currentUser.role === 'user';
    
    userCustomers.forEach((c, index) => {
        const status = getSafeValue(c, 'الحالة') || 'قيد الاعتماد';
        let statusClass = 'badge-pending';
        if (status === 'معتمد') statusClass = 'badge-approved';
        else if (status === 'مرفوض') statusClass = 'badge-rejected';
        
        const rejectionReason = getSafeValue(c, 'سبب_الرفض');
        const rejectionButton = (status === 'مرفوض' && rejectionReason) ? 
            `<button onclick="showRejectionReason('${escapeHtml(rejectionReason)}')" class="text-red-500 hover:text-red-600 p-1 hover:bg-red-50 rounded-lg mr-1" title="سبب الرفض">
                <i class="ri-error-warning-line text-lg"></i>
            </button>` : '';
        
        const canEdit = (status !== 'معتمد' && usernameMatches(getSafeValue(c, 'الموظف'), currentUser.username)) || currentUser.role === 'admin';
        
        let attachmentValue = getSafeValue(c, 'المرفق') || getSafeValue(c, 'المرفقات') || getSafeValue(c, 'attachment') || getSafeValue(c, 'attachments') || '';
        const hasAttachments = attachmentValue.length > 0;
        
        let attachmentsCell = hasAttachments ? `
            <button onclick="showAttachments('${escapeHtml(attachmentValue)}')" 
                    class="inline-flex items-center justify-center gap-1 px-3 py-2 bg-primary/10 hover:bg-primary/20 text-primary hover:text-primaryDark rounded-lg transition-all duration-200 group" 
                    title="عرض المرفقات">
                <i class="ri-attachment-line text-lg group-hover:scale-110 transition-transform"></i>
                <span class="text-xs font-medium">${attachmentValue.split(',').filter(f => f.trim()).length}</span>
            </button>
        ` : '<span class="text-gray-300">-</span>';
        
        const tr = document.createElement('tr');
        tr.className = 'hover:bg-gray-50 transition-colors border-b border-gray-100 last:border-b-0';
        tr.innerHTML = `
            ${!isUser ? `<td class="px-4 py-3 text-center"><input type="checkbox" class="customer-checkbox custom-checkbox" value="${getSafeValue(c, 'معرف')}"></td>` : ''}
            <td class="px-4 py-3 text-center">
                ${rejectionButton}
                <button onclick='showDocumentPreview(${JSON.stringify(c).replace(/'/g, "&apos;")}, "customer")' 
                        class="inline-flex items-center justify-center w-10 h-10 bg-amber-50 hover:bg-amber-100 text-amber-500 hover:text-amber-600 rounded-full transition-all duration-200" 
                        title="عرض التفاصيل">
                    <i class="ri-arrow-left-s-line text-2xl"></i>
                </button>
            </td>
            <td class="px-4 py-3 text-center font-sm text-gray-600">${index + 1}</td>
            <td class="px-4 py-3 text-center text-sm text-gray-600">${formatDate(getSafeValue(c, 'التاريخ'))}</td>
            ${!isUser ? `<td class="px-4 py-3 text-center text-sm font-medium text-gray-700">${getSafeValue(c, 'الموظف')}</td>` : ''}
            <td class="px-4 py-3 text-center text-sm text-gray-600">${getSafeValue(c, 'اسم_العميل') || getSafeValue(c, 'اسم العميل') || '-'}</td>
            <td class="px-4 py-3 text-center text-sm text-gray-600">${getSafeValue(c, 'نوع_العميل') || '-'}</td>
            <td class="px-4 py-3 text-center"><span class="badge ${statusClass}">${status}</span></td>
            <td class="px-4 py-3 text-sm text-gray-600 max-w-xs truncate" title="${getSafeValue(c, 'الملاحظات') || ''}">${getSafeValue(c, 'الملاحظات') || '-'}</td>
            <td class="px-4 py-3 text-center">${attachmentsCell}</td>
            ${canEdit ? `<td class="px-4 py-3 text-center">
                <div class="flex items-center justify-center gap-1">
                    <button onclick="editCustomer('${getSafeValue(c, 'معرف')}')" 
                            class="inline-flex items-center justify-center w-9 h-9 bg-blue-50 hover:bg-blue-100 text-blue-500 hover:text-blue-600 rounded-lg transition-all duration-200" 
                            title="تعديل">
                        <i class="ri-edit-line text-lg"></i>
                    </button>
                    <button onclick="deleteCustomer('${getSafeValue(c, 'معرف')}')" 
                            class="inline-flex items-center justify-center w-9 h-9 bg-red-50 hover:bg-red-100 text-red-500 hover:text-red-600 rounded-lg transition-all duration-200" 
                            title="حذف">
                        <i class="ri-delete-bin-line text-lg"></i>
                    </button>
                </div>
            </td>` : '<td class="px-4 py-3 text-center text-gray-400">-</td>'}
        `;
        fragment.appendChild(tr);
    });
    
    table.innerHTML = '';
    table.appendChild(fragment);
}

function updateSalesTable() {
    const adminTable = document.getElementById('admin-all-sales-table');
    const userTable = document.getElementById('my-sales-table');
    
    const userSales = appCache.data.sales.filter(s => 
        currentUser.role === 'admin' || 
        usernameMatches(getSafeValue(s, 'الموظف'), currentUser.username)
    );
    
    const renderRow = (s, index, isAdmin) => {
        const status = getSafeValue(s, 'الحالة');
        let statusClass = 'badge-pending';
        if (status === 'معتمد') statusClass = 'badge-approved';
        else if (status === 'مرفوض') statusClass = 'badge-rejected';
        
        const rejectionReason = getSafeValue(s, 'سبب_الرفض');
        const rejectionButton = (status === 'مرفوض' && rejectionReason) ? 
            `<button onclick="showRejectionReason('${escapeHtml(rejectionReason)}')" class="text-red-500 hover:text-red-600 p-1 hover:bg-red-50 rounded-lg mr-1">
                <i class="ri-error-warning-line text-lg"></i>
            </button>` : '';
        
        const canEdit = status !== 'معتمد' && usernameMatches(getSafeValue(s, 'الموظف'), currentUser.username);
        
        let itemsSummary = '-';
        try {
            const items = JSON.parse(getSafeValue(s, 'تفاصيل_الأصناف') || '[]');
            itemsSummary = items.length > 0 ? `${items.length} صنف` : '-';
        } catch(e) {}
        
        const base = `
            <td class="text-center">
                ${rejectionButton}
                <button onclick='showDocumentPreview(${JSON.stringify(s).replace(/'/g, "&apos;")}, "sale")' class="text-amber-500 hover:text-amber-600">
                    <i class="ri-arrow-left-s-line text-2xl"></i>
                </button>
            </td>
            <td>${index + 1}</td>
            <td>${formatDate(getSafeValue(s, 'التاريخ'))}</td>
            ${isAdmin ? `<td>${getSafeValue(s, 'الموظف')}</td>` : ''}
            <td>${getSafeValue(s, 'العميل')}</td>
            <td>${itemsSummary}</td>
            <td>${getSafeValue(s, 'مكان_التصنيع') || '-'}</td>
            <td>${getSafeValue(s, 'طريقة_السداد') || '-'}</td>
            <td>${getSafeValue(s, 'مكان_التسليم') || '-'}</td>
            <td><span class="badge ${statusClass}">${status}</span></td>
            <td>${getSafeValue(s, 'الملاحظات') || '-'}</td>
        `;
        
        if (isAdmin) {
            return `<tr><td class="text-center"><input type="checkbox" class="sale-checkbox custom-checkbox" value="${getSafeValue(s, 'معرف')}"></td>${base}</tr>`;
        } else {
            return `<tr>${base}${canEdit ? `<td>
                <button onclick="editSale('${getSafeValue(s, 'معرف')}')" class="text-blue-500 hover:text-blue-600 mr-2"><i class="ri-edit-line"></i></button>
                <button onclick="deleteSale('${getSafeValue(s, 'معرف')}')" class="text-red-500 hover:text-red-600"><i class="ri-delete-bin-line"></i></button>
            </td>` : '<td>-</td>'}</tr>`;
        }
    };
    
    if (adminTable) {
        adminTable.innerHTML = userSales.map((s, i) => renderRow(s, i, true)).join('') || '<tr><td colspan="11" class="text-center py-8">لا توجد بيانات</td></tr>';
    }
    
    if (userTable) {
        userTable.innerHTML = userSales.map((s, i) => renderRow(s, i, false)).join('') || '<tr><td colspan="11" class="text-center py-8">لا توجد بيانات</td></tr>';
    }
}

function updateQuotesTable() {
    const adminTable = document.getElementById('admin-all-quotes-table');
    const userTable = document.getElementById('my-quotes-table');
    
    const userQuotes = appCache.data.quotes.filter(q => 
        currentUser.role === 'admin' || 
        usernameMatches(getSafeValue(q, 'الموظف'), currentUser.username)
    );
    
    const renderRow = (q, index, isAdmin) => {
        const status = getSafeValue(q, 'الحالة');
        let statusClass = 'badge-pending';
        if (status === 'معتمد') statusClass = 'badge-approved';
        else if (status === 'مرفوض') statusClass = 'badge-rejected';
        
        let itemsSummary = '-';
        try {
            const items = JSON.parse(getSafeValue(q, 'تفاصيل_الأصناف') || '[]');
            itemsSummary = items.length > 0 ? `${items.length} صنف` : '-';
        } catch(e) {}
        
        const canEdit = status !== 'معتمد' && usernameMatches(getSafeValue(q, 'الموظف'), currentUser.username);
        
        const base = `
            <td class="text-center">
                <button onclick='showDocumentPreview(${JSON.stringify(q).replace(/'/g, "&apos;")}, "quote")' class="text-amber-500 hover:text-amber-600">
                    <i class="ri-arrow-left-s-line text-2xl"></i>
                </button>
            </td>
            <td>${index + 1}</td>
            <td>${formatDate(getSafeValue(q, 'التاريخ'))}</td>
            ${isAdmin ? `<td>${getSafeValue(q, 'الموظف')}</td>` : ''}
            <td>${getSafeValue(q, 'العميل')}</td>
            <td>${itemsSummary}</td>
            <td>${getSafeValue(q, 'طريقة_السداد') || '-'}</td>
            <td>${getSafeValue(q, 'مكان_التسليم') || '-'}</td>
            <td><span class="badge ${statusClass}">${status}</span></td>
        `;
        
        if (isAdmin) {
            return `<tr><td class="text-center"><input type="checkbox" class="quote-checkbox custom-checkbox" value="${getSafeValue(q, 'معرف')}"></td>${base}</tr>`;
        } else {
            return `<tr>${base}${canEdit ? `<td>
                <button onclick="editQuote('${getSafeValue(q, 'معرف')}')" class="text-blue-500 hover:text-blue-600 mr-2"><i class="ri-edit-line"></i></button>
                <button onclick="deleteQuote('${getSafeValue(q, 'معرف')}')" class="text-red-500 hover:text-red-600"><i class="ri-delete-bin-line"></i></button>
            </td>` : '<td>-</td>'}</tr>`;
        }
    };
    
    if (adminTable) {
        adminTable.innerHTML = userQuotes.map((q, i) => renderRow(q, i, true)).join('') || '<tr><td colspan="9" class="text-center py-8">لا توجد بيانات</td></tr>';
    }
    
    if (userTable) {
        userTable.innerHTML = userQuotes.map((q, i) => renderRow(q, i, false)).join('') || '<tr><td colspan="9" class="text-center py-8">لا توجد بيانات</td></tr>';
    }
}

function updateComplaintsTable() {
    const adminTable = document.getElementById('admin-all-complaints-table');
    const userTable = document.getElementById('my-complaints-table');
    
    const userComplaints = appCache.data.complaints.filter(c => 
        currentUser.role === 'admin' || 
        usernameMatches(getSafeValue(c, 'الموظف'), currentUser.username)
    );
    
    const renderRow = (c, index, isAdmin) => {
        const status = getSafeValue(c, 'الحالة');
        let statusClass = 'badge-pending';
        if (status === 'معتمد') statusClass = 'badge-approved';
        else if (status === 'مرفوض') statusClass = 'badge-rejected';
        
        let attachmentsHtml = '-';
        const attachmentsRaw = getSafeValue(c, 'المرفق');
        if (attachmentsRaw && typeof attachmentsRaw === 'string' && attachmentsRaw.trim() !== '') {
            const urls = attachmentsRaw.split(',').filter(u => u.trim() !== '');
            if (urls.length > 0) {
                attachmentsHtml = `<button onclick="showAttachments('${escapeHtml(attachmentsRaw)}')" class="text-primary hover:text-primaryDark">
                                        <i class="ri-attachment-2-line text-xl"></i>
                                    </button>`;
            }
        }
        
        const base = `
            <td class="text-center">
                <button onclick='showDocumentPreview(${JSON.stringify(c).replace(/'/g, "&apos;")}, "complaint")' class="text-amber-500 hover:text-amber-600">
                    <i class="ri-arrow-left-s-line text-2xl"></i>
                </button>
            </td>
            <td>${index + 1}</td>
            <td>${formatDate(getSafeValue(c, 'التاريخ'))}</td>
            ${isAdmin ? `<td>${getSafeValue(c, 'الموظف')}</td>` : ''}
            <td>${getSafeValue(c, 'العميل')}</td>
            <td>${getSafeValue(c, 'الكمية') || '-'}</td>
            <td>${getSafeValue(c, 'الوحدة') || '-'}</td>
            <td>${getSafeValue(c, 'رقم_الهاتف') || '-'}</td>
            <td>${getSafeValue(c, 'مسؤول_التواصل') || '-'}</td>
            <td>${getSafeValue(c, 'رقم_مسؤول_التواصل') || '-'}</td>
            <td>${getSafeValue(c, 'طريقة_الشكوى') || '-'}</td>
            <td>${getSafeValue(c, 'النوع') || '-'}</td>
            <td><span class="badge ${statusClass}">${status}</span></td>
            <td>${getSafeValue(c, 'الوصف') || '-'}</td>
            <td>${attachmentsHtml}</td>
        `;
        
        if (isAdmin) {
            return `<tr><td class="text-center"><input type="checkbox" class="complaint-checkbox custom-checkbox" value="${getSafeValue(c, 'معرف')}">${base}</tr>`;
        } else {
            return `<tr>${base}</tr>`;
        }
    };
    
    if (adminTable) {
        adminTable.innerHTML = userComplaints.map((c, i) => renderRow(c, i, true)).join('') || '<tr><td colspan="15" class="text-center py-8">لا توجد بيانات</td></tr>';
    }
    if (userTable) {
        userTable.innerHTML = userComplaints.map((c, i) => renderRow(c, i, false)).join('') || '<tr><td colspan="15" class="text-center py-8">لا توجد بيانات</td></tr>';
    }
}

function updateVisitsTable() {
    const adminTable = document.getElementById('admin-visits-table');
    const userTable = document.getElementById('my-visits-table');
    
    const userVisits = appCache.data.visits.filter(v => 
        currentUser.role === 'admin' || 
        usernameMatches(getSafeValue(v, 'الموظف'), currentUser.username)
    );
    
    const renderRow = (v, index, isAdmin) => `
        <tr>
            <td class="text-center">
                <button onclick='showDocumentPreview(${JSON.stringify(v).replace(/'/g, "&apos;")}, "visit")' class="text-amber-500 hover:text-amber-600">
                    <i class="ri-arrow-left-s-line text-2xl"></i>
                </button>
            </td>
            <td>${index + 1}</td>
            <td>${formatDate(getSafeValue(v, 'التاريخ'))}</td>
            ${isAdmin ? `<td>${getSafeValue(v, 'الموظف')}</td>` : ''}
            <td>${getSafeValue(v, 'العميل')}</td>
            <td>${getSafeValue(v, 'الموقع') || '-'}</td>
            <td>${formatTimeOnly(getSafeValue(v, 'وقت_الدخول'))}</td>
            <td>${formatTimeOnly(getSafeValue(v, 'وقت_الخروج'))}</td>
            <td>${getSafeValue(v, 'الغرض') || '-'}</td>
            <td>${getSafeValue(v, 'النتيجة') || '-'}</td>
            <td>${getSafeValue(v, 'الملاحظات') || '-'}</td>
        </tr>
    `;
    
    if (adminTable) {
        adminTable.innerHTML = userVisits.map((v, i) => renderRow(v, i, true)).join('') || '<tr><td colspan="11" class="text-center py-8">لا توجد بيانات</td></tr>';
    }
    
    if (userTable) {
        userTable.innerHTML = userVisits.map((v, i) => renderRow(v, i, false)).join('') || '<tr><td colspan="10" class="text-center py-8">لا توجد بيانات</td></tr>';
    }
}

function updateActivitiesTable() {
  const adminTable = document.getElementById('admin-activities-table');
  const userTable = document.getElementById('my-activities-table');
  
  const userActivities = appCache.data.activities.filter(a => 
      currentUser.role === 'admin' || 
      usernameMatches(getSafeValue(a, 'الموظف'), currentUser.username)
  );
  
  const renderRow = (a, index, isAdmin) => {
      let detailsSummary = '-';
      let totalSales = 0;
      let totalCollection = 0;
      let detailsCount = 0;
      
      try {
          const detailsRaw = getSafeValue(a, 'تفاصيل_النشاطات');
          const details = typeof detailsRaw === 'string' ? JSON.parse(detailsRaw) : (detailsRaw || []);
          detailsCount = details.length;
          detailsSummary = detailsCount > 0 ? `${detailsCount} نشاط` : '-';
          
          // حساب الإجماليات من التفاصيل
          details.forEach(d => {
              totalSales += parseFloat(d.salesToday) || 0;
              totalCollection += parseFloat(d.collectionToday) || 0;
          });
      } catch(e) {
          console.error('خطأ في تحليل تفاصيل النشاط:', e);
      }
      
      // استخدام الإجماليات المحفوظة مباشرة إذا وجدت
      const savedTotalSales = parseFloat(getSafeValue(a, 'إجمالي_مبيعات_اليوم')) || totalSales;
      const savedTotalCollection = parseFloat(getSafeValue(a, 'إجمالي_تحصيل_اليوم')) || totalCollection;
      const notes = getSafeValue(a, 'ملاحظات') || '-';
      const activityDate = getSafeValue(a, 'التاريخ');
      const employee = getSafeValue(a, 'الموظف');
      
      return `
          <tr class="hover:bg-gray-50 transition-colors border-b border-gray-100">
              <td class="px-4 py-3 text-center">
                  <button onclick='showDocumentPreview(${JSON.stringify(a).replace(/'/g, "&apos;")}, "activity")' 
                          class="inline-flex items-center justify-center w-9 h-9 bg-amber-50 hover:bg-amber-100 text-amber-500 hover:text-amber-600 rounded-lg transition-all duration-200"
                          title="عرض التفاصيل">
                      <i class="ri-eye-line text-lg"></i>
                  </button>
              </td>
              <td class="px-4 py-3 text-center font-medium text-gray-700">${index + 1}</td>
              <td class="px-4 py-3 text-center text-sm text-gray-600">${formatDate(activityDate)}</td>
              ${isAdmin ? `<td class="px-4 py-3 text-center text-sm font-medium text-gray-700">${employee || '-'}</td>` : ''}
              <td class="px-4 py-3 text-center text-sm">
                  <span class="inline-flex items-center gap-1 px-2 py-1 bg-blue-100 text-blue-700 rounded-full text-xs font-medium">
                      <i class="ri-file-list-line"></i> ${detailsSummary}
                  </span>
              </td>
              <td class="px-4 py-3 text-center">
                  <span class="font-bold text-blue-600 text-sm">${savedTotalSales.toFixed(2)}</span>
                  <span class="text-xs text-gray-500"> ج.م</span>
              </td>
              <td class="px-4 py-3 text-center">
                  <span class="font-bold text-green-600 text-sm">${savedTotalCollection.toFixed(2)}</span>
                  <span class="text-xs text-gray-500"> ج.م</span>
              </td>
              <td class="px-4 py-3 text-sm text-gray-600 max-w-xs truncate" title="${notes}">${notes.length > 30 ? notes.substring(0, 30) + '...' : notes}</td>
          </tr>
      `;
  };
  
  if (adminTable) {
      if (userActivities.length === 0) {
          adminTable.innerHTML = '<tr><td colspan="8" class="text-center py-12 text-gray-500">لا توجد أنشطة مسجلة</td></tr>';
      } else {
          adminTable.innerHTML = userActivities.map((a, i) => renderRow(a, i, true)).join('');
      }
  }
  
  if (userTable) {
      if (userActivities.length === 0) {
          userTable.innerHTML = '<tr><td colspan="7" class="text-center py-12 text-gray-500">لا توجد أنشطة مسجلة</td></tr>';
      } else {
          userTable.innerHTML = userActivities.map((a, i) => renderRow(a, i, false)).join('');
      }
  }
}

function updatePlansTable() {
    const table = document.getElementById('my-plans-table');
    if (!table) return;
    
    const userPlans = appCache.data.plans.filter(p => 
        currentUser.role === 'admin' || 
        usernameMatches(getSafeValue(p, 'الموظف'), currentUser.username)
    );
    
    table.innerHTML = userPlans.map((p, index) => `
        <tr>
            <td class="text-center">
                <button onclick='showDocumentPreview(${JSON.stringify(p).replace(/'/g, "&apos;")}, "plan")' class="text-amber-500 hover:text-amber-600">
                    <i class="ri-arrow-left-s-line text-2xl"></i>
                </button>
            </td>
            <td>${index + 1}</td>
            <td>${formatDate(getSafeValue(p, 'من_تاريخ') || getSafeValue(p, 'من تاريخ'), true)}</td>
            <td>${formatDate(getSafeValue(p, 'إلى_تاريخ') || getSafeValue(p, 'إلى تاريخ'), true)}</td>
            <td>${getSafeValue(p, 'الأهداف') || '-'}</td>
            <td>${getSafeValue(p, 'المهام') || '-'}</td>
            <td>${getSafeValue(p, 'الملاحظات') || '-'}</td>
        </tr>
    `).join('') || '<tr><td colspan="7" class="text-center py-8">لا توجد بيانات</td></tr>';
}

function updateCollectionsTable() {
    const table = document.getElementById('my-collections-table');
    if (!table) return;
    
    const userCollections = appCache.data.collections.filter(c => 
        currentUser.role === 'admin' || 
        usernameMatches(getSafeValue(c, 'الموظف'), currentUser.username)
    );
    
    table.innerHTML = userCollections.map((c, index) => `
        <tr>
            <td class="text-center">
                <button onclick='showDocumentPreview(${JSON.stringify(c).replace(/'/g, "&apos;")}, "collection")' class="text-amber-500 hover:text-amber-600">
                    <i class="ri-arrow-left-s-line text-2xl"></i>
                </button>
            </td>
            <td>${index + 1}</td>
            <td>${formatDate(getSafeValue(c, 'التاريخ'))}</td>
            <td>${getSafeValue(c, 'العميل')}</td>
            <td>${getSafeValue(c, 'المبلغ_المستحق') || '-'} ج.م</td>
            <td>${formatDate(getSafeValue(c, 'تاريخ_الاستحقاق'), true)}</td>
            <td><span class="badge ${getSafeValue(c, 'الحالة') === 'مدفوع' ? 'badge-approved' : getSafeValue(c, 'الحالة') === 'متأخر' ? 'badge-rejected' : 'badge-pending'}">${getSafeValue(c, 'الحالة') || '-'}</span></td>
            <td>${getSafeValue(c, 'الملاحظات') || '-'}</td>
        </tr>
    `).join('') || '<tr><td colspan="8" class="text-center py-8">لا توجد بيانات</td></tr>';
}

function updateUsersTable() {
    const table = document.getElementById('users-list');
    if (!table) return;
    
    // إضافة class text-center للجدول بأكمله
    table.closest('table')?.classList.add('w-full');
    
    table.innerHTML = appCache.data.users.map(u => `
        <tr class="hover:bg-gray-50 transition-colors">
            <td class="px-6 py-4 text-center font-medium">${escapeHtml(u.username)}</td>
            <td class="px-6 py-4 text-center">
                <span class="badge ${u.role === 'admin' ? 'badge-approved' : u.role === 'manager' ? 'badge-pending' : 'badge-pending'}">
                    ${u.role === 'admin' ? 'مسؤول' : u.role === 'manager' ? 'مدير' : 'موظف'}
                </span>
            </td>
            <td class="px-6 py-4 text-center">
                <div class="flex items-center justify-center gap-2">
                    <button onclick="editUser('${escapeHtml(u.username)}')" 
                            class="inline-flex items-center justify-center w-8 h-8 bg-blue-50 hover:bg-blue-100 text-blue-500 hover:text-blue-600 rounded-lg transition-all duration-200">
                        <i class="ri-edit-line text-lg"></i>
                    </button>
                    <button onclick="deleteUser('${escapeHtml(u.username)}')" 
                            class="inline-flex items-center justify-center w-8 h-8 bg-red-50 hover:bg-red-100 text-red-500 hover:text-red-600 rounded-lg transition-all duration-200">
                        <i class="ri-delete-bin-line text-lg"></i>
                    </button>
                </div>
            </td>
        </tr>
    `).join('') || '<tr><td colspan="3" class="px-6 py-12 text-center text-gray-500">لا يوجد موظفين</td></tr>';
}

function updatePendingUsersTable() {
    const table = document.getElementById('pending-users-table');
    if (!table) return;
    
    const pendingUsers = appCache.data.pendingUsers || [];
    
    if (pendingUsers.length === 0) {
        table.innerHTML = `
            <tr>
                <td colspan="4" class="px-6 py-12 text-center text-gray-500">
                    <div class="flex flex-col items-center gap-2">
                        <i class="ri-inbox-line text-4xl text-gray-300"></i>
                        <span>لا توجد طلبات مستخدمين جديدة</span>
                    </div>
                </td>
            </tr>
        `;
        return;
    }
    
    table.innerHTML = pendingUsers.map(user => `
        <tr class="hover:bg-gray-50 transition-colors">
            <td class="px-6 py-4 text-sm font-medium text-gray-900">${escapeHtml(user.username)}</td>
            <td class="px-6 py-4 text-sm text-gray-600">${escapeHtml(user.email)}</td>
            <td class="px-6 py-4 text-sm text-gray-600">${formatDate(user.requestDate)}</td>
            <td class="px-6 py-4 text-sm">
                <div class="flex gap-2">
                    <button onclick="approveUser('${user.username}')" 
                            class="inline-flex items-center gap-1 px-3 py-1.5 bg-green-500 hover:bg-green-600 text-white rounded-lg text-sm font-medium transition-all">
                        <i class="ri-check-line"></i>
                        <span>اعتماد</span>
                    </button>
                    <button onclick="rejectUser('${user.username}')" 
                            class="inline-flex items-center gap-1 px-3 py-1.5 bg-red-500 hover:bg-red-600 text-white rounded-lg text-sm font-medium transition-all">
                        <i class="ri-close-line"></i>
                        <span>رفض</span>
                    </button>
                </div>
            </td>
        </tr>
    `).join('');
}

function updateActivitiesLog() {
    const table = document.getElementById('activities-log');
    if (!table) return;
    
    const userStats = {};
    
    const updateStats = (data, key, field) => {
        data.forEach(item => {
            const user = getSafeValue(item, 'الموظف');
            if (!userStats[user]) userStats[user] = { customers: 0, plans: 0, visits: 0, activities: 0, quotes: 0, sales: 0, complaints: 0, collections: 0, lastActivity: '' };
            userStats[user][key]++;
            const date = getSafeValue(item, 'التاريخ');
            if (date > userStats[user].lastActivity) userStats[user].lastActivity = date;
        });
    };
    
    updateStats(appCache.data.customers, 'customers');
    updateStats(appCache.data.plans, 'plans');
    updateStats(appCache.data.visits, 'visits');
    updateStats(appCache.data.activities, 'activities');
    updateStats(appCache.data.quotes, 'quotes');
    updateStats(appCache.data.sales, 'sales');
    updateStats(appCache.data.complaints, 'complaints');
    updateStats(appCache.data.collections, 'collections');
    
    table.innerHTML = Object.entries(userStats).map(([user, stats]) => `
        <tr>
            <td class="font-bold">${user}</td>
            <td>${stats.customers}</td>
            <td>${stats.plans}</td>
            <td>${stats.visits}</td>
            <td>${stats.activities}</td>
            <td>${stats.quotes}</td>
            <td>${stats.sales}</td>
            <td>${stats.complaints}</td>
            <td>${stats.collections}</td>
            <td>${formatDate(stats.lastActivity)}</td>
        </tr>
    `).join('') || '<tr><td colspan="10" class="text-center py-8">لا توجد بيانات</td></tr>';
}

// ═══════════════════════════════════════════════════════════════════════════
// القسم الرابع عشر: تهيئة التطبيق والأحداث (محسنة)
// ═══════════════════════════════════════════════════════════════════════════

function logout() {
    currentUser = null;
    localStorage.removeItem('hyma_currentUser');
    appCache.clear();
    customersMap.clear();
    itemsMap.clear();
    fieldMapCache.clear();
    dateFormatCache.clear();
    docTemplateCache.clear();
    escapeHtmlCache.clear();
    idCounters.clear();
    pendingSaves.clear();
    dropdownsInitialized = false;
    showPage('login-page');
}

function init() {
    const storedMessages = localStorage.getItem('hyma_adminMessages');
    if (storedMessages) {
        try { adminMessages = JSON.parse(storedMessages); } catch(e) {}
    }
    const storedSpeed = localStorage.getItem('hyma_marqueeSpeed');
    if (storedSpeed) {
        document.documentElement.style.setProperty('--marquee-duration', storedSpeed + 's');
    }
    updateMessagesMarquee();

    const savedUser = localStorage.getItem('hyma_currentUser');
    if (savedUser) {
        try {
            currentUser = JSON.parse(savedUser);
            loadAllData();
            if (currentUser.role === 'admin' || currentUser.role === 'manager') {
                showPage('admin-page');
            } else {
                showPage('user-page');
            }
        } catch (e) { 
            showPage('login-page');
        }
    } else {
        showPage('login-page');
    }
    
    const basedOnBtn = document.getElementById('based-on-docs-btn');
    if (basedOnBtn) basedOnBtn.addEventListener('click', openBasedOnModal);
    
    document.querySelectorAll('.tax-radio-quote').forEach(radio => {
        radio.addEventListener('change', () => calculateQuoteTotals());
    });
    
}

// ═══════════════════════════════════════════════════════════════════════════
// دوال زر "مبني على" في النشاط اليومي
// ═══════════════════════════════════════════════════════════════════════════

function compareDatesOnly(dateStr1, dateStr2) {
    try {
        const d1 = new Date(dateStr1);
        const d2 = new Date(dateStr2);
        if (isNaN(d1) || isNaN(d2)) return false;
        return d1.getFullYear() === d2.getFullYear() &&
               d1.getMonth() === d2.getMonth() &&
               d1.getDate() === d2.getDate();
    } catch(e) {
        const clean1 = String(dateStr1).trim().substring(0,10);
        const clean2 = String(dateStr2).trim().substring(0,10);
        return clean1 === clean2;
    }
}

function openBasedOnModal() {
    const btn = document.getElementById('based-on-docs-btn');
    if (!btn) return;
    
    const originalHTML = btn.innerHTML;
    btn.disabled = true;
    btn.innerHTML = '<i class="ri-loader-4-line animate-spin"></i> جاري التحميل...';

    const dateInput = document.getElementById('activity-date');
    let selectedDateISO = dateInput?.value;
    
    if (!selectedDateISO) {
        const today = new Date();
        selectedDateISO = `${today.getFullYear()}-${String(today.getMonth()+1).padStart(2,'0')}-${String(today.getDate()).padStart(2,'0')}`;
    }
    
    console.log('🔍 البحث عن مستندات بتاريخ:', selectedDateISO);

    const docsContainer = document.getElementById('documents-list');
    if (docsContainer) {
        docsContainer.innerHTML = '<div class="text-center py-8"><i class="ri-loader-4-line animate-spin text-3xl text-primary"></i><p class="mt-2">جاري التحميل...</p></div>';
    }
    
    const modal = document.getElementById('based-on-modal');
    if (modal) modal.classList.remove('hidden');

    loadAllData(true).then(() => {
        try {
            const categories = [
                { name: 'أوامر البيع', data: appCache.data.sales, clientField: 'العميل', docName: 'أمر بيع' },
                { name: 'عروض الأسعار', data: appCache.data.quotes, clientField: 'العميل', docName: 'عرض سعر' },
                { name: 'شكاوى العملاء', data: appCache.data.complaints, clientField: 'العميل', docName: 'شكوى' },
                { name: 'زيارات العملاء', data: appCache.data.visits, clientField: 'العميل', docName: 'تقرير زيارة' },
                { name: 'التحصيلات', data: appCache.data.collections, clientField: 'العميل', docName: 'متابعة تحصيل' }
            ];

            let html = '';
            let totalCount = 0;

            categories.forEach(cat => {
                if (!cat.data || !Array.isArray(cat.data)) return;

                const userDocs = cat.data.filter(doc => {
                    const docUser = getSafeValue(doc, 'الموظف');
                    const isOwner = currentUser.role === 'admin' || 
                                   currentUser.role === 'manager' ||
                                   usernameMatches(docUser, currentUser.username);
                    if (!isOwner) return false;
                    
                    const docDateRaw = getSafeValue(doc, 'التاريخ');
                    if (!docDateRaw) return false;
                    
                    return compareDatesOnly(docDateRaw, selectedDateISO);
                });

                if (userDocs.length === 0) return;
                
                totalCount += userDocs.length;

                html += `
                    <div class="flex-shrink-0 w-80 bg-white border border-gray-200 rounded-xl p-4 shadow-sm">
                        <div class="font-bold text-lg mb-3 text-primary border-b pb-2 flex justify-between items-center">
                            <span>${cat.name}</span>
                            <span class="bg-primary text-white text-xs px-2 py-1 rounded-full">${userDocs.length}</span>
                        </div>
                        <div class="space-y-2 max-h-80 overflow-y-auto">
                `;

                userDocs.forEach(doc => {
                    const docId = getSafeValue(doc, 'معرف') || '';
                    let clientName = getSafeValue(doc, cat.clientField) || 
                                    getSafeValue(doc, 'العميل') || 
                                    'غير محدد';
                    
                    const safeClientName = clientName.replace(/"/g, '&quot;').replace(/'/g, "\\'");
                    
                    html += `
                        <div onclick="selectDocument('${cat.docName}', '${docId}', '${safeClientName}', '${cat.docName}')" 
                             class="bg-gray-50 hover:bg-primary/10 border border-gray-200 hover:border-primary rounded-lg p-3 cursor-pointer transition-all group">
                            <div class="flex justify-between items-center mb-1">
                                <span class="font-semibold text-sm text-gray-800 group-hover:text-primary">${cat.docName}</span>
                                <span class="text-xs text-gray-500">${formatDate(getSafeValue(doc, 'التاريخ'))}</span>
                            </div>
                            <div class="text-sm text-gray-600 mb-1 flex items-center gap-1">
                                <i class="ri-user-line text-primary"></i>
                                <span class="font-medium">${clientName}</span>
                            </div>
                            <div class="text-xs text-gray-400">رقم: ${docId}</div>
                        </div>
                    `;
                });

                html += `</div></div>`;
            });

            if (html === '') {
                if (docsContainer) {
                    docsContainer.innerHTML = `
                        <div class="text-center py-12 w-full text-gray-500">
                            <i class="ri-inbox-line text-4xl mb-3 block text-gray-300"></i>
                            <p class="font-medium">لا توجد مستندات بتاريخ ${formatDate(selectedDateISO, true)}</p>
                            <p class="text-sm mt-2 text-gray-400">تأكد من وجود مستندات (مبيعات، عروض أسعار، شكاوى، زيارات، تحصيلات) لهذا التاريخ.</p>
                        </div>
                    `;
                }
            } else {
                if (docsContainer) docsContainer.innerHTML = html;
            }

        } catch (err) {
            console.error('❌ خطأ في معالجة البيانات:', err);
            if (docsContainer) docsContainer.innerHTML = '<div class="text-center py-8 text-red-500">حدث خطأ أثناء تحميل البيانات</div>';
        }
    }).catch(err => {
        console.error('❌ خطأ في تحميل البيانات:', err);
        if (docsContainer) docsContainer.innerHTML = '<div class="text-center py-8 text-red-500">فشل الاتصال بالخادم</div>';
    }).finally(() => {
        btn.disabled = false;
        btn.innerHTML = originalHTML;
    });
}

function selectDocument(docType, docId, clientName, displayName) {
    console.log('🎯 اختيار مستند:', { docType, docId, clientName, displayName });
    
    let finalDocName = displayName;
    if (!finalDocName || finalDocName === 'undefined' || /^\d+$/.test(finalDocName)) {
        finalDocName = docType;
        console.log('⚠️ displayName كان رقمًا، تم استخدام docType بدلاً منه:', finalDocName);
    }
    
    const tbody = document.getElementById('activities-detail-body');
    if (!tbody) {
        console.error('❌ جدول الأنشطة غير موجود');
        return;
    }

    let emptyRow = null;
    for (let row of tbody.children) {
        const typeInput = row.querySelector('.activity-type');
        const clientSelect = row.querySelector('.activity-client-select');
        const reasonInput = row.querySelector('.activity-reason');
        
        const typeVal = typeInput?.value?.trim() || '';
        let clientVal = '';
        if (clientSelect) {
            const selectedOption = clientSelect.options[clientSelect.selectedIndex];
            clientVal = selectedOption ? selectedOption.text.trim() : '';
        }
        const reasonVal = reasonInput?.value?.trim() || '';
        
        if (!typeVal && !clientVal && !reasonVal) {
            emptyRow = row;
            break;
        }
    }

    let targetRow = emptyRow;
    if (!targetRow) {
        console.log('➕ لا يوجد صف فارغ، إضافة صف جديد');
        addActivityRow();
        targetRow = tbody.lastElementChild;
    }

    if (!targetRow) return;

    const typeInput = targetRow.querySelector('.activity-type');
    const clientSelect = targetRow.querySelector('.activity-client-select');
    const timeFromInput = targetRow.querySelector('.activity-time-from');

    if (typeInput) {
        typeInput.value = finalDocName;
        typeInput.dispatchEvent(new Event('input', { bubbles: true }));
    }

    if (clientName && clientName !== 'غير محدد' && clientSelect) {
        let optionExists = false;
        for (let i = 0; i < clientSelect.options.length; i++) {
            if (clientSelect.options[i].text === clientName) {
                clientSelect.selectedIndex = i;
                optionExists = true;
                break;
            }
        }
        if (!optionExists) {
            const option = document.createElement('option');
            option.value = clientName;
            option.text = clientName;
            clientSelect.appendChild(option);
            clientSelect.value = clientName;
        }
        clientSelect.dispatchEvent(new Event('change', { bubbles: true }));

        const wrapper = clientSelect.parentElement?.querySelector('.searchable-wrapper') || 
                       clientSelect.closest('.searchable-wrapper');
        if (wrapper) {
            const searchInput = wrapper.querySelector('input[type="text"]');
            if (searchInput) {
                searchInput.value = clientName;
                const dropdown = wrapper.querySelector('.dropdown-suggestions');
                if (dropdown) dropdown.classList.add('hidden');
            }
        }
    }

    if (timeFromInput && !timeFromInput.value) {
        const now = new Date();
        timeFromInput.value = `${String(now.getHours()).padStart(2, '0')}:${String(now.getMinutes()).padStart(2, '0')}`;
    }

    closeBasedOnModal();
    showSuccess(`تم إضافة ${finalDocName} للعميل ${clientName || ''}`);
}

function closeBasedOnModal() {
    const modal = document.getElementById('based-on-modal');
    if (modal) modal.classList.add('hidden');
}

// ═══════════════════════════════════════════════════════════════════════════
// معرف تسلسلي (محسن)
// ═══════════════════════════════════════════════════════════════════════════

async function generateSequentialId(prefix, sheetName, idField = 'معرف') {
    const cacheKey = `${prefix}-${sheetName}`;
    if (idCounters.has(cacheKey)) {
        const current = idCounters.get(cacheKey);
        idCounters.set(cacheKey, current + 1);
        return `${prefix}${String(current + 1).padStart(4, '0')}`;
    }
    
    try {
        const res = await sendRequest({ action: 'GET', sheetName });
        if (!res.success || !res.data) return `${prefix}0001`;
        
        let maxNum = 0;
        res.data.forEach(row => {
            const id = row[idField];
            if (id && String(id).startsWith(prefix)) {
                const num = parseInt(String(id).replace(prefix, ''), 10);
                if (!isNaN(num) && num > maxNum) maxNum = num;
            }
        });
        
        idCounters.set(cacheKey, maxNum);
        return `${prefix}${String(maxNum + 1).padStart(4, '0')}`;
    } catch (err) {
        console.error('خطأ في توليد المعرف:', err);
        return `${prefix}${Date.now().toString().slice(-4)}`;
    }
}

// ═══════════════════════════════════════════════════════════════════════════
// إغلاق نافذة معاينة المستند وطباعته
// ═══════════════════════════════════════════════════════════════════════════

function closePreviewModal() {
    const modal = document.getElementById('preview-modal');
    if (modal) modal.classList.add('hidden');
}

function printPreview() {
    const previewContent = document.getElementById('preview-content');
    if (!previewContent) {
        showError('لا يوجد محتوى للطباعة');
        return;
    }

    const originalTitle = document.title;
    document.title = 'طباعة المستند';

    const printWindow = window.open('', '_blank');
    if (!printWindow) {
        showError('الرجاء السماح بالنوافذ المنبثقة للمتصفح');
        return;
    }

    const styles = document.querySelector('style')?.innerHTML || '';
    const printContent = `
        <!DOCTYPE html>
        <html dir="rtl">
        <head>
            <meta charset="UTF-8">
            <title>طباعة المستند</title>
            <style>
                @import url('https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700&display=swap');
                
                body {
                    font-family: 'Tajawal', sans-serif;
                    margin: 0;
                    padding: 20px;
                    background: white;
                    direction: rtl;
                }
                .doc-container {
                    max-width: 210mm;
                    margin: 0 auto;
                    background: white;
                }
                .doc-totals, .doc-amount-words, .doc-signatures, .doc-footer {
                    display: block !important;
                }
                table {
                    border-collapse: collapse;
                    width: 100%;
                }
                th, td {
                    border: 1px solid #333;
                    padding: 8px;
                }
                .doc-grand-total {
                    font-weight: bold;
                    color: #198a11;
                }
                @media print {
                    body {
                        margin: 0;
                        padding: 0;
                    }
                    .doc-container {
                        margin: 0;
                        padding: 10mm;
                    }
                    button, .no-print {
                        display: none !important;
                    }
                }
            </style>
        </head>
        <body>
            ${previewContent.innerHTML}
        </body>
        </html>
    `;

    printWindow.document.write(printContent);
    printWindow.document.close();
    printWindow.focus();
    printWindow.print();

    document.title = originalTitle;
}

// ═══════════════════════════════════════════════════════════════════════════
// أحداث النماذج الرئيسية
// ═══════════════════════════════════════════════════════════════════════════

document.addEventListener('DOMContentLoaded', () => {
    init();
    
    // Event delegation للجداول
    document.body.addEventListener('click', (e) => {
        const target = e.target.closest('button, [onclick]');
        if (!target) return;
    });
    
    // مراقبة تغييرات DOM للصفحات
    const observer = new MutationObserver((mutations) => {
        mutations.forEach((mutation) => {
            if (mutation.type === 'attributes' && mutation.attributeName === 'class') {
                const target = mutation.target;
                if (target.id === 'add-activity-page' && !target.classList.contains('hidden')) {
                    const dateField = document.getElementById('activity-date');
                    if (dateField && !dateField.value) {
                        dateField.value = new Date().toISOString().split('T')[0];
                    }
                }
            }
        });
    });
    
    document.querySelectorAll('[id$="-page"]').forEach(page => {
        observer.observe(page, { attributes: true });
    });
});

// نموذج تسجيل الدخول
document.getElementById('login-form')?.addEventListener('submit', async function(e) {
    e.preventDefault();
    const username = document.getElementById('username')?.value.trim();
    const password = document.getElementById('password')?.value;
    if (!username || !password) return showError('يرجى إدخال البيانات');
    
    const btn = document.getElementById('login-btn');
    const orig = btn?.innerText;
    if (btn) {
        btn.innerText = 'جاري تسجيل الدخول...';
        btn.disabled = true;
    }
    
    try {
        const res = await sendRequest({ action: 'LOGIN', username, password });
        if (res.success) {
            currentUser = res.data;
            localStorage.setItem('hyma_currentUser', JSON.stringify(currentUser));
            loadAllData();
            if (currentUser.role === 'admin' || currentUser.role === 'manager') {
                showPage('admin-page');
            } else {
                showPage('user-page');
            }
        } else {
            showError(res.message || 'فشل تسجيل الدخول');
        }
    } catch (err) {
        showError('خطأ في الاتصال: ' + err.message);
    } finally {
        if (btn) {
            btn.innerText = orig;
            btn.disabled = false;
        }
    }
});

// رابط التسجيل
document.getElementById('register-link')?.addEventListener('click', e => {
    e.preventDefault();
    document.getElementById('login-form')?.classList.add('hidden');
    document.getElementById('register-form')?.classList.remove('hidden');
    document.getElementById('login-link-container')?.classList.remove('hidden');
});

document.getElementById('login-link')?.addEventListener('click', e => {
    e.preventDefault();
    document.getElementById('login-form')?.classList.remove('hidden');
    document.getElementById('register-form')?.classList.add('hidden');
    document.getElementById('login-link-container')?.classList.add('hidden');
});

// نموذج التسجيل
document.getElementById('register-form')?.addEventListener('submit', async function(e) {
    e.preventDefault();
    const username = document.getElementById('register-username')?.value.trim();
    const email = document.getElementById('register-email')?.value.trim();
    const password = document.getElementById('register-password')?.value;
    const confirmPassword = document.getElementById('register-confirm-password')?.value;
    
    if (!username || !email || !password) return showError('جميع الحقول مطلوبة');
    if (password !== confirmPassword) return showError('كلمات المرور غير متطابقة');
    
    const btn = this.querySelector('button[type="submit"]');
    const orig = btn?.innerText;
    if (btn) {
        btn.innerText = 'جاري إرسال الطلب...';
        btn.disabled = true;
    }
    
    try {
        const res = await sendRequest({ 
            action: 'REGISTER', 
            username, 
            email, 
            password 
        });
        if (res.success) {
            showSuccess('تم إرسال طلبك، سيتم مراجعته من قبل المسؤول');
            document.getElementById('register-form')?.classList.add('hidden');
            document.getElementById('login-form')?.classList.remove('hidden');
            document.getElementById('login-link-container')?.classList.add('hidden');
            document.getElementById('register-form')?.reset();
        } else {
            showError(res.message || 'فشل التسجيل');
        }
    } catch (err) {
        showError('خطأ في الاتصال: ' + err.message);
    } finally {
        if (btn) {
            btn.innerText = orig;
            btn.disabled = false;
        }
    }
});

// نموذج الملف الشخصي
document.getElementById('profile-form')?.addEventListener('submit', async function(e) {
    e.preventDefault();
    const username = document.getElementById('profile-username')?.value.trim();
    const email = document.getElementById('profile-email')?.value.trim();
    const password = document.getElementById('profile-password')?.value;
    const confirmPassword = document.getElementById('profile-confirm-password')?.value;
    
    if (!username || !email) return showError('اسم المستخدم والبريد مطلوبان');
    if (password && password !== confirmPassword) return showError('كلمات المرور غير متطابقة');
    
    try {
        const res = await sendRequest({ 
            action: 'UPDATE_PROFILE', 
            oldUsername: currentUser.username,
            username, 
            email, 
            password: password || null
        });
        if (res.success) {
            currentUser.username = username;
            currentUser.email = email;
            localStorage.setItem('hyma_currentUser', JSON.stringify(currentUser));
            showSuccess('تم تحديث البيانات');
            loadUserData();
        } else {
            showError(res.message || 'فشل التحديث');
        }
    } catch (err) {
        showError('خطأ في الاتصال: ' + err.message);
    }
});

// نموذج تعديل المستخدم
document.getElementById('edit-user-form')?.addEventListener('submit', async function(e) {
    e.preventDefault();
    const originalUsername = document.getElementById('edit-original-username')?.value;
    const username = document.getElementById('edit-username')?.value.trim();
    const email = document.getElementById('edit-email')?.value.trim();
    const role = document.querySelector('input[name="edit-role"]:checked')?.value;
    const password = document.getElementById('edit-password')?.value;
    
    if (!username || !email || !role) return showError('جميع الحقول مطلوبة');
    
    try {
        const res = await sendRequest({ 
            action: 'UPDATE_USER', 
            originalUsername,
            username, 
            email, 
            role,
            password: password || null
        });
        if (res.success) {
            showSuccess('تم تحديث المستخدم');
            document.getElementById('edit-user-modal')?.classList.add('hidden');
            loadAllData(true);
        } else {
            showError(res.message || 'فشل التحديث');
        }
    } catch (err) {
        showError('خطأ في الاتصال: ' + err.message);
    }
});

// ربط نماذج الحفظ
document.getElementById('customer-form')?.addEventListener('submit', saveCustomer);
document.getElementById('plan-form')?.addEventListener('submit', savePlan);
document.getElementById('visit-form')?.addEventListener('submit', saveVisit);
document.getElementById('activity-form')?.addEventListener('submit', saveActivity);
document.getElementById('quote-form')?.addEventListener('submit', saveQuote);
document.getElementById('sale-form')?.addEventListener('submit', saveSale);
document.getElementById('complaint-form')?.addEventListener('submit', saveComplaint);
document.getElementById('collection-form')?.addEventListener('submit', saveCollection);

// ═══════════════════════════════════════════════════════════════════════════
// دوال الرسائل (Success / Error)
// ═══════════════════════════════════════════════════════════════════════════

function showSuccess(message) {
    const modal = document.getElementById('success-modal');
    const msgSpan = document.getElementById('success-msg');
    if (modal && msgSpan) {
        msgSpan.textContent = message;
        modal.classList.remove('hidden');
        setTimeout(() => {
            modal.classList.add('hidden');
        }, 3000);
    } else {
        alert('✅ ' + message);
    }
}

function showError(message) {
    const modal = document.getElementById('error-modal');
    const msgSpan = document.getElementById('error-msg');
    if (modal && msgSpan) {
        msgSpan.textContent = message;
        modal.classList.remove('hidden');
        setTimeout(() => {
            modal.classList.add('hidden');
        }, 3000);
    } else {
        alert('❌ ' + message);
    }
}

// ═══════════════════════════════════════════════════════════════════════════
// ربط أحداث الأزرار الرئيسية
// ═══════════════════════════════════════════════════════════════════════════

document.getElementById('add-customer-btn')?.addEventListener('click', () => {
    isEditingCustomer = false;
    editingCustomerId = null;
    document.getElementById('customer-form')?.reset();
    const idField = document.getElementById('customer-id');
    if (idField) idField.value = '';
    showPage('add-customer-page');
});

document.getElementById('add-plan-btn')?.addEventListener('click', () => {
    document.getElementById('plan-form')?.reset();
    showPage('add-plan-page');
});

document.getElementById('add-visit-btn')?.addEventListener('click', () => {
    document.getElementById('visit-form')?.reset();
    const locField = document.getElementById('visit-location');
    if (locField) locField.value = '';
    showPage('add-visit-page');
});

document.getElementById('add-activity-btn')?.addEventListener('click', () => {
    const tbody = document.getElementById('activities-detail-body');
    if (tbody) tbody.innerHTML = '';
    addActivityRow(); // إضافة صف فارغ
    showPage('add-activity-page');
    
    // تعبئة التاريخ والموظف تلقائياً
    const dateField = document.getElementById('activity-date');
    if (dateField) {
        dateField.value = new Date().toISOString().split('T')[0];
    }
    
    const employeeField = document.getElementById('activity-employee');
    if (employeeField && currentUser) {
        employeeField.value = currentUser.username;
    }
});

document.getElementById('add-quote-btn')?.addEventListener('click', () => {
    isEditingQuote = false;
    editingQuoteId = null;
    document.getElementById('quote-form')?.reset();
    const itemsBody = document.getElementById('quote-items-body');
    if (itemsBody) itemsBody.innerHTML = '';
    addQuoteItemRow();
    const dateField = document.getElementById('quote-date');
    if (dateField) dateField.value = new Date().toISOString().split('T')[0];
    showPage('add-quote-page');
});

document.getElementById('add-sale-btn')?.addEventListener('click', () => {
    isEditingSale = false;
    editingSaleId = null;
    document.getElementById('sale-form')?.reset();
    const itemsBody = document.getElementById('sale-items-body');
    if (itemsBody) itemsBody.innerHTML = '';
    addSaleItemRow();
    const dateField = document.getElementById('sale-date');
    if (dateField) dateField.value = new Date().toISOString().split('T')[0];
    calculateSaleTotals();
    showPage('add-sales-page');
});

document.getElementById('add-complaint-btn')?.addEventListener('click', () => {
    document.getElementById('complaint-form')?.reset();
    showPage('add-complaint-page');
});

document.getElementById('add-collection-btn')?.addEventListener('click', () => {
    document.getElementById('collection-form')?.reset();
    showPage('add-collection-page');
});

document.getElementById('get-location-btn')?.addEventListener('click', getLocation);

document.getElementById('user-logout')?.addEventListener('click', logout);
document.getElementById('admin-logout')?.addEventListener('click', logout);

document.getElementById('close-preview-modal')?.addEventListener('click', closePreviewModal);
document.getElementById('print-preview-btn')?.addEventListener('click', printPreview);

document.getElementById('based-on-docs-btn')?.addEventListener('click', openBasedOnModal);

// دالة إظهار Toast بدلاً من Alert
function showToast(message, type = 'success') {
    const toast = document.createElement('div');
    toast.className = `fixed bottom-4 left-4 z-50 flex items-center gap-3 px-4 py-3 rounded-xl shadow-lg animate-slide-up ${
        type === 'success' ? 'bg-success' : 
        type === 'error' ? 'bg-danger' : 
        'bg-info'
    } text-white`;
    toast.innerHTML = `<i class="ri-${type === 'success' ? 'check-line' : type === 'error' ? 'close-line' : 'information-line'} text-xl"></i><span>${message}</span>`;
    document.body.appendChild(toast);
    setTimeout(() => toast.remove(), 3000);
}

// تعديل دوال showSuccess و showError لاستخدام Toast
window.showSuccess = showToast;
window.showError = (msg) => showToast(msg, 'error');

// دالة تبديل الوضع الليلي
function toggleDarkMode() {
    document.documentElement.classList.toggle('dark');
    localStorage.setItem('darkMode', document.documentElement.classList.contains('dark'));
}

// تحميل الوضع المحفوظ
if (localStorage.getItem('darkMode') === 'true') {
    document.documentElement.classList.add('dark');
}

// زر تبديل الوضع الليلي (يمكن إضافته في الشريط العلوي)
// <button onclick="toggleDarkMode()" class="hover:bg-white/20 p-2 rounded-xl"><i class="ri-moon-line text-xl"></i></button>

// ==============================================
// دوال القائمة المنسدلة للملف الشخصي
// ==============================================

function toggleProfileDropdown(event) {
    event?.stopPropagation();
    const dropdown = document.getElementById('profile-dropdown');
    if (dropdown) {
        dropdown.classList.toggle('hidden');
    }
}

function closeProfileDropdown() {
    const dropdown = document.getElementById('profile-dropdown');
    if (dropdown) {
        dropdown.classList.add('hidden');
    }
}



// ==============================================
// دوال التنبيهات والإشعارات
// ==============================================

let notifications = [];

// إضافة إشعار جديد
function addNotification(message, type = 'info') {
    const id = Date.now() + Math.random();
    notifications.unshift({ 
        id: id.toString(), 
        message: message, 
        type: type, 
        read: false, 
        timestamp: new Date().toISOString() 
    });
    
    // الاحتفاظ بآخر 50 إشعار فقط
    if (notifications.length > 50) notifications.pop();
    
    // حفظ في localStorage
    localStorage.setItem('hyma_notifications', JSON.stringify(notifications));
    
    // تحديث الواجهة
    updateNotifBadge();
    renderNotificationsList();
}

// تحديث عدد الإشعارات غير المقروءة
function updateNotifBadge() {
    const unread = notifications.filter(n => !n.read).length;
    const badge = document.getElementById('notif-badge-count');
    
    if (badge) {
        if (unread > 0) {
            badge.classList.remove('hidden');
            badge.innerText = unread > 9 ? '9+' : unread;
        } else {
            badge.classList.add('hidden');
        }
    }
}

// عرض قائمة الإشعارات
function renderNotificationsList() {
    const container = document.getElementById('notifications-list');
    if (!container) return;
    
    if (notifications.length === 0) {
        container.innerHTML = '<div class="p-4 text-center text-gray-500">لا توجد إشعارات</div>';
        return;
    }
    
    container.innerHTML = notifications.map(n => `
        <div class="notif-item p-3 border-b hover:bg-gray-50 dark:hover:bg-gray-700 cursor-pointer ${!n.read ? 'bg-yellow-50 dark:bg-yellow-900/20' : ''}" 
             onclick="markNotificationRead('${n.id}')">
            <div class="flex items-start gap-3">
                <i class="ri-${n.type === 'success' ? 'check-circle-line' : n.type === 'danger' ? 'alert-line' : 'information-line'} text-lg ${n.type === 'success' ? 'text-green-500' : n.type === 'danger' ? 'text-red-500' : 'text-primary'}"></i>
                <div class="flex-1">
                    <p class="text-sm text-gray-700 dark:text-gray-300">${escapeHtml(n.message)}</p>
                    <p class="text-xs text-gray-400 mt-1">${formatTimeAgo(n.timestamp)}</p>
                </div>
            </div>
        </div>
    `).join('');
}

// تحديد إشعار كمقروء
function markNotificationRead(id) {
    const notification = notifications.find(n => n.id == id);
    if (notification) {
        notification.read = true;
        localStorage.setItem('hyma_notifications', JSON.stringify(notifications));
        updateNotifBadge();
        renderNotificationsList();
    }
}

// مسح جميع الإشعارات
function clearAllNotifications() {
    if (confirm('هل أنت متأكد من مسح جميع الإشعارات؟')) {
        notifications = [];
        localStorage.setItem('hyma_notifications', JSON.stringify(notifications));
        updateNotifBadge();
        renderNotificationsList();
        showToast('تم مسح جميع الإشعارات', 'success');
    }
}

// فتح/إغلاق لوحة الإشعارات
function toggleNotificationsPanel(event) {
    event?.stopPropagation();
    const panel = document.getElementById('notifications-dropdown');
    if (panel) {
        panel.classList.toggle('hidden');
        renderNotificationsList();
    }
}

function closeNotificationsPanel() {
    const panel = document.getElementById('notifications-dropdown');
    if (panel) {
        panel.classList.add('hidden');
    }
}

// حساب الوقت المنقضي (منذ كم دقيقة/ساعة/يوم)
function formatTimeAgo(timestamp) {
    const now = new Date();
    const date = new Date(timestamp);
    const diffMs = now - date;
    const diffMins = Math.floor(diffMs / 60000);
    const diffHours = Math.floor(diffMs / 3600000);
    const diffDays = Math.floor(diffMs / 86400000);
    
    if (diffMins < 1) return 'الآن';
    if (diffMins < 60) return `منذ ${diffMins} دقيقة`;
    if (diffHours < 24) return `منذ ${diffHours} ساعة`;
    return `منذ ${diffDays} يوم`;
}

// تهيئة الإشعارات (تحميل المحفوظة)
function initNotifications() {
    const savedNotifs = localStorage.getItem('hyma_notifications');
    if (savedNotifs) {
        try {
            notifications = JSON.parse(savedNotifs);
            updateNotifBadge();
        } catch(e) {
            console.error('خطأ في تحميل الإشعارات', e);
        }
    }
    
    // ربط الأحداث
    const notifBell = document.getElementById('notif-bell');
    if (notifBell) {
        notifBell.addEventListener('click', toggleNotificationsPanel);
    }
    
    // إغلاق اللوحة عند النقر خارجها
    document.addEventListener('click', (e) => {
        if (!e.target.closest('#notif-bell') && !e.target.closest('#notifications-dropdown')) {
            closeNotificationsPanel();
        }
    });
}

// إشعارات تلقائية (محاكاة - يمكن تفعيلها حسب الحاجة)
function startAutoNotifications() {
    // مثال: إشعار كل 30 ثانية (للاختبار فقط)
    setInterval(() => {
        // يمكن تفعيل هذا للإشعارات التلقائية
        // addNotification('تذكير: هناك مستندات في انتظار المراجعة', 'info');
    }, 30000);
}

// ==============================================
// دوال مساعدة
// ==============================================

// تحويل النص إلى HTML آمن
function escapeHtml(text) {
    if (!text) return '';
    const div = document.createElement('div');
    div.textContent = text;
    return div.innerHTML;
}

// إشعارات عند اعتماد/رفض المستندات
function addDocumentNotification(type, action, count, reason = '') {
    const typeName = type === 'sale' ? 'أمر بيع' : 
                     type === 'quote' ? 'عرض سعر' : 
                     type === 'complaint' ? 'شكوى' : 'مستند';
    
    const actionName = action === 'approve' ? 'اعتماد' : 'رفض';
    let message = `تم ${actionName} ${count} من ${typeName}`;
    
    if (action === 'reject' && reason) {
        message += ` (السبب: ${reason.substring(0, 50)}${reason.length > 50 ? '...' : ''})`;
    }
    
    addNotification(message, action === 'approve' ? 'success' : 'danger');
}

// إشعار عند رفع قائمة أسعار جديدة
function notifyNewPriceList() {
    addNotification('📄 هناك قائمة أسعار جديدة متاحة للاطلاع', 'info');
}

// ==============================================
// دوال التقارير الشاملة
// ==============================================

// 1. جلب جميع العناصر من جميع الجداول لتوليد التقرير
function getAllReportItems() {
    let items = [];
    
    // إضافة أوامر البيع
    const addSales = (arr) => {
        arr.forEach(item => {
            items.push({
                type: 'أمر بيع',
                id: getSafeValue(item, 'معرف'),
                date: getSafeValue(item, 'التاريخ'),
                client: getSafeValue(item, 'العميل'),
                employee: getSafeValue(item, 'الموظف'),
                status: getSafeValue(item, 'الحالة'),
                rawData: item
            });
        });
    };
    
    // إضافة عروض الأسعار
    const addQuotes = (arr) => {
        arr.forEach(item => {
            items.push({
                type: 'عرض سعر',
                id: getSafeValue(item, 'معرف'),
                date: getSafeValue(item, 'التاريخ'),
                client: getSafeValue(item, 'العميل'),
                employee: getSafeValue(item, 'الموظف'),
                status: getSafeValue(item, 'الحالة'),
                rawData: item
            });
        });
    };
    
    // إضافة شكاوى العملاء
    const addComplaints = (arr) => {
        arr.forEach(item => {
            items.push({
                type: 'شكوى',
                id: getSafeValue(item, 'معرف'),
                date: getSafeValue(item, 'التاريخ'),
                client: getSafeValue(item, 'العميل'),
                employee: getSafeValue(item, 'الموظف'),
                status: getSafeValue(item, 'الحالة'),
                rawData: item
            });
        });
    };
    
    // إضافة العملاء
    const addCustomers = (arr) => {
        arr.forEach(item => {
            items.push({
                type: 'عميل',
                id: getSafeValue(item, 'معرف'),
                date: getSafeValue(item, 'التاريخ'),
                client: getSafeValue(item, 'اسم_العميل') || getSafeValue(item, 'اسم العميل'),
                employee: getSafeValue(item, 'الموظف'),
                status: getSafeValue(item, 'الحالة'),
                rawData: item
            });
        });
    };
    
    // إضافة زيارات العملاء
    const addVisits = (arr) => {
        arr.forEach(item => {
            items.push({
                type: 'زيارة',
                id: getSafeValue(item, 'معرف'),
                date: getSafeValue(item, 'التاريخ'),
                client: getSafeValue(item, 'العميل'),
                employee: getSafeValue(item, 'الموظف'),
                status: getSafeValue(item, 'الحالة') || 'مكتملة',
                rawData: item
            });
        });
    };
    
    // إضافة الأنشطة اليومية
    const addActivities = (arr) => {
        arr.forEach(item => {
            items.push({
                type: 'نشاط يومي',
                id: getSafeValue(item, 'معرف'),
                date: getSafeValue(item, 'التاريخ'),
                client: '-',
                employee: getSafeValue(item, 'الموظف'),
                status: 'مكتمل',
                rawData: item
            });
        });
    };
    
    // إضافة الخطط الأسبوعية
    const addPlans = (arr) => {
        arr.forEach(item => {
            items.push({
                type: 'خطة أسبوعية',
                id: getSafeValue(item, 'معرف'),
                date: getSafeValue(item, 'من_تاريخ') || getSafeValue(item, 'من تاريخ'),
                client: '-',
                employee: getSafeValue(item, 'الموظف'),
                status: 'مخطط',
                rawData: item
            });
        });
    };
    
    // إضافة التحصيلات
    const addCollections = (arr) => {
        arr.forEach(item => {
            items.push({
                type: 'تحصيل',
                id: getSafeValue(item, 'معرف'),
                date: getSafeValue(item, 'التاريخ'),
                client: getSafeValue(item, 'العميل'),
                employee: getSafeValue(item, 'الموظف'),
                status: getSafeValue(item, 'الحالة'),
                rawData: item
            });
        });
    };
    
    // تنفيذ الإضافات إذا كانت البيانات موجودة
    if (appCache.data.sales) addSales(appCache.data.sales);
    if (appCache.data.quotes) addQuotes(appCache.data.quotes);
    if (appCache.data.complaints) addComplaints(appCache.data.complaints);
    if (appCache.data.customers) addCustomers(appCache.data.customers);
    if (appCache.data.visits) addVisits(appCache.data.visits);
    if (appCache.data.activities) addActivities(appCache.data.activities);
    if (appCache.data.plans) addPlans(appCache.data.plans);
    if (appCache.data.collections) addCollections(appCache.data.collections);
    
    // ترتيب حسب التاريخ (الأحدث أولاً)
    items.sort((a, b) => new Date(b.date) - new Date(a.date));
    
    return items;
}

// 2. تطبيق الفلترة على التقارير
function applyReportsFilter() {
    const clientFilter = document.getElementById('report-filter-client')?.value.trim().toLowerCase() || '';
    const fromDate = document.getElementById('report-filter-date-from')?.value;
    const toDate = document.getElementById('report-filter-date-to')?.value;
    const statusFilter = document.getElementById('report-filter-status')?.value || 'all';
    const typeFilter = document.getElementById('report-filter-type')?.value || 'all';
    
    let allItems = getAllReportItems();
    
    let filtered = allItems.filter(item => {
        // فلترة باسم العميل
        if (clientFilter && !item.client?.toLowerCase().includes(clientFilter)) return false;
        
        // فلترة بالتاريخ من
        if (fromDate && item.date && new Date(item.date) < new Date(fromDate)) return false;
        
        // فلترة بالتاريخ إلى
        if (toDate && item.date && new Date(item.date) > new Date(toDate)) return false;
        
        // فلترة بالحالة
        if (statusFilter !== 'all' && item.status !== statusFilter) return false;
        
        // فلترة بالنوع
        if (typeFilter !== 'all' && item.type !== typeFilter) return false;
        
        return true;
    });
    
    renderReportsTable(filtered);
    updateReportSummary(filtered);
}

// 3. عرض جدول التقارير
function renderReportsTable(items) {
    const tbody = document.getElementById('reports-table-body');
    if (!tbody) return;
    
    if (items.length === 0) {
        tbody.innerHTML = `
            <tr>
                <td colspan="7" class="text-center py-12 text-gray-500">
                    <i class="ri-inbox-line text-5xl mb-3 block text-gray-300"></i>
                    <p>لا توجد بيانات مطابقة للبحث</p>
                </td>
            </tr>
        `;
        return;
    }
    
    tbody.innerHTML = items.map((item, index) => {
        let statusClass = '';
        let statusText = item.status || 'قيد الاعتماد';
        
        if (statusText === 'معتمد') statusClass = 'badge-approved';
        else if (statusText === 'مرفوض') statusClass = 'badge-rejected';
        else statusClass = 'badge-pending';
        
        // تحديد نوع المستند لعرضه بشكل صحيح
        let docTypeForPreview = '';
        if (item.type === 'أمر بيع') docTypeForPreview = 'sale';
        else if (item.type === 'عرض سعر') docTypeForPreview = 'quote';
        else if (item.type === 'شكوى') docTypeForPreview = 'complaint';
        else if (item.type === 'عميل') docTypeForPreview = 'customer';
        else if (item.type === 'زيارة') docTypeForPreview = 'visit';
        else if (item.type === 'نشاط يومي') docTypeForPreview = 'activity';
        else if (item.type === 'خطة أسبوعية') docTypeForPreview = 'plan';
        else if (item.type === 'تحصيل') docTypeForPreview = 'collection';
        
        return `
            <tr class="hover:bg-gray-50 dark:hover:bg-gray-700/50 transition-colors border-b border-gray-100 dark:border-gray-700">
                <td class="px-4 py-3">
                    <span class="inline-flex items-center gap-2">
                        <i class="ri-${getIconForType(item.type)} text-primary"></i>
                        ${item.type}
                    </span>
                </td>
                <td class="px-4 py-3 font-mono text-sm">${item.id || '-'}</td>
                <td class="px-4 py-3">${formatDate(item.date)}</td>
                <td class="px-4 py-3">${item.client || '-'}</td>
                <td class="px-4 py-3">${item.employee || '-'}</td>
                <td class="px-4 py-3">
                    <span class="badge ${statusClass}">${statusText}</span>
                </td>
                <td class="px-4 py-3 text-center">
                    <button onclick='showDocumentPreview(${JSON.stringify(item.rawData).replace(/'/g, "&apos;")}, "${docTypeForPreview}")' 
                            class="inline-flex items-center justify-center w-9 h-9 bg-amber-50 hover:bg-amber-100 text-amber-500 hover:text-amber-600 rounded-lg transition-all duration-200"
                            title="عرض التفاصيل">
                        <i class="ri-eye-line text-lg"></i>
                    </button>
                </td>
            </tr>
        `;
    }).join('');
}

// 4. الحصول على أيقونة حسب نوع المستند
function getIconForType(type) {
    const icons = {
        'أمر بيع': 'shopping-cart-line',
        'عرض سعر': 'file-list-line',
        'شكوى': 'alert-line',
        'عميل': 'user-line',
        'زيارة': 'map-pin-line',
        'نشاط يومي': 'calendar-check-line',
        'خطة أسبوعية': 'calendar-todo-line',
        'تحصيل': 'money-dollar-circle-line'
    };
    return icons[type] || 'file-line';
}

// 5. تحديث ملخص التقرير (إحصائيات)
function updateReportSummary(items) {
    const summaryEl = document.getElementById('report-summary');
    if (!summaryEl) return;
    
    const total = items.length;
    const approved = items.filter(i => i.status === 'معتمد').length;
    const pending = items.filter(i => i.status === 'قيد الاعتماد').length;
    const rejected = items.filter(i => i.status === 'مرفوض').length;
    
    summaryEl.innerHTML = `
        <div class="flex flex-wrap gap-4 p-4 bg-gray-50 dark:bg-gray-800 rounded-xl">
            <div class="flex items-center gap-2">
                <div class="w-3 h-3 rounded-full bg-primary"></div>
                <span class="text-sm">الإجمالي: ${total}</span>
            </div>
            <div class="flex items-center gap-2">
                <div class="w-3 h-3 rounded-full bg-green-500"></div>
                <span class="text-sm">معتمد: ${approved}</span>
            </div>
            <div class="flex items-center gap-2">
                <div class="w-3 h-3 rounded-full bg-yellow-500"></div>
                <span class="text-sm">قيد الاعتماد: ${pending}</span>
            </div>
            <div class="flex items-center gap-2">
                <div class="w-3 h-3 rounded-full bg-red-500"></div>
                <span class="text-sm">مرفوض: ${rejected}</span>
            </div>
        </div>
    `;
}

// 6. إعادة ضبط الفلاتر
function resetReportsFilter() {
    document.getElementById('report-filter-client').value = '';
    document.getElementById('report-filter-date-from').value = '';
    document.getElementById('report-filter-date-to').value = '';
    if (document.getElementById('report-filter-status')) {
        document.getElementById('report-filter-status').value = 'all';
    }
    if (document.getElementById('report-filter-type')) {
        document.getElementById('report-filter-type').value = 'all';
    }
    applyReportsFilter();
}

// 7. تصدير التقارير إلى Excel
function exportFilteredReports() {
    const clientFilter = document.getElementById('report-filter-client')?.value.trim().toLowerCase() || '';
    const fromDate = document.getElementById('report-filter-date-from')?.value;
    const toDate = document.getElementById('report-filter-date-to')?.value;
    
    let allItems = getAllReportItems();
    let filtered = allItems.filter(item => {
        if (clientFilter && !item.client?.toLowerCase().includes(clientFilter)) return false;
        if (fromDate && item.date && new Date(item.date) < new Date(fromDate)) return false;
        if (toDate && item.date && new Date(item.date) > new Date(toDate)) return false;
        return true;
    });
    
    if (filtered.length === 0) {
        showToast('لا توجد بيانات للتصدير', 'error');
        return;
    }
    
    const exportData = filtered.map(item => ({
        'النوع': item.type,
        'رقم المستند': item.id,
        'التاريخ': formatDate(item.date),
        'العميل': item.client || '-',
        'الموظف': item.employee || '-',
        'الحالة': item.status || 'قيد الاعتماد'
    }));
    
    const ws = XLSX.utils.json_to_sheet(exportData);
    const wb = XLSX.utils.book_new();
    XLSX.utils.book_append_sheet(wb, ws, 'التقارير');
    XLSX.writeFile(wb, `تقرير_${new Date().toISOString().slice(0, 19).replace(/:/g, '-')}.xlsx`);
    
    showToast('تم تصدير التقرير بنجاح', 'success');
}

// 8. تحميل بيانات التقارير
function loadReportsData() {
    // التأكد من وجود البيانات في الكاش
    if (!appCache.data.sales || !appCache.data.customers) {
        loadAllData().then(() => {
            applyReportsFilter();
        });
    } else {
        applyReportsFilter();
    }
}

// 9. عرض صفحة التقارير
function showReportsPage() {
    showPage('reports-page');
    loadReportsData();
}

// 10. طباعة التقرير
function printReport() {
    const printContent = document.getElementById('reports-table-body')?.innerHTML;
    const headers = document.querySelector('#reports-page .modern-table thead')?.innerHTML;
    
    if (!printContent) return;
    
    const printWindow = window.open('', '_blank');
    printWindow.document.write(`
        <!DOCTYPE html>
        <html dir="rtl">
        <head>
            <meta charset="UTF-8">
            <title>تقرير Hyma Plastic</title>
            <style>
                body { font-family: 'Tajawal', sans-serif; padding: 20px; }
                table { width: 100%; border-collapse: collapse; }
                th, td { border: 1px solid #ddd; padding: 8px; text-align: right; }
                th { background: #f5f5f5; }
                .header { text-align: center; margin-bottom: 20px; }
            </style>
        </head>
        <body>
            <div class="header">
                <h2>Hyma Plastic - تقرير شامل</h2>
                <p>تاريخ التقرير: ${new Date().toLocaleDateString('ar-EG')}</p>
            </div>
            <table>
                <thead>${headers}</thead>
                <tbody>${printContent}</tbody>
            </table>
        </body>
        </html>
    `);
    printWindow.document.close();
    printWindow.print();
}

// إغلاق جميع القوائم عند النقر خارجها (نسخة مختصرة)
document.addEventListener('click', function(e) {
    // إغلاق قائمة الملف الشخصي
    const profileBtn = document.getElementById('profile-btn');
    const profileDropdown = document.getElementById('profile-dropdown');
    if (profileDropdown && !profileDropdown.contains(e.target) && !profileBtn?.contains(e.target)) {
        profileDropdown.classList.add('hidden');
    }
    
    // إغلاق لوحة الإشعارات
    const notifBell = document.getElementById('notif-bell');
    const notifPanel = document.getElementById('notifications-dropdown');
    if (notifPanel && !notifPanel.contains(e.target) && !notifBell?.contains(e.target)) {
        notifPanel.classList.add('hidden');
    }
});


// ═══════════════════════════════════════════════════════════════════════════
// دوال مساعدة إضافية
// ═══════════════════════════════════════════════════════════════════════════

function renumberActivityRows() {
    const rows = document.querySelectorAll('#activities-detail-body tr');
    rows.forEach((row, index) => {
        const numCell = row.querySelector('td:first-child');
        if (numCell) {
            numCell.textContent = index + 1;
        }
    });
}

(function ensureAdminVisibility() {
    // تنفيذ فوري
    if (currentUser && currentUser.role === 'admin') {
        const row = document.getElementById('admin-only-row');
        if (row) row.classList.remove('hidden');
    }
    
    // مراقبة التغييرات
    const observer = new MutationObserver(function() {
        if (currentUser && currentUser.role === 'admin') {
            const row = document.getElementById('admin-only-row');
            if (row && row.classList.contains('hidden')) {
                row.classList.remove('hidden');
                console.log('🔧 تم إظهار قسم الأدمن تلقائياً');
            }
        }
    });
    
    observer.observe(document.body, { 
        attributes: true, 
        childList: true, 
        subtree: true,
        attributeFilter: ['class']
    });
})();
// ═══════════════════════════════════════════════════════════════════════════
// تصدير الدوال للنطاق العام
// ═══════════════════════════════════════════════════════════════════════════

window.showSuccess = showSuccess;
window.showError = showError;
window.logout = logout;
window.init = init;
window.editCustomer = editCustomer;
window.deleteCustomer = deleteCustomer;
window.editQuote = editQuote;
window.deleteQuote = deleteQuote;
window.editSale = editSale;
window.deleteSale = deleteSale;
window.editUser = editUser;
window.deleteUser = deleteUser;
window.approveUser = approveUser;
window.rejectUser = rejectUser;
window.approveSelected = approveSelected;
window.rejectSelected = rejectSelected;
window.approveSelectedCustomers = approveSelectedCustomers;
window.rejectSelectedCustomers = rejectSelectedCustomers;
window.closeRejectionModal = closeRejectionModal;
window.confirmRejection = confirmRejection;
window.showRejectionReason = showRejectionReason;
window.showAttachments = showAttachments;
window.openEmailModal = openEmailModal;
window.closeEmailModal = closeEmailModal;
window.openExportFilterModal = openExportFilterModal;
window.closeExportFilterModal = closeExportFilterModal;
window.exportFilteredData = exportFilteredData;
window.openPriceListModal = openPriceListModal;
window.closePriceListModal = closePriceListModal;
window.uploadPriceList = uploadPriceList;
window.showPriceList = showPriceList;
window.openMessagesModal = openMessagesModal;
window.closeMessagesModal = closeMessagesModal;
window.saveMessages = saveMessages;
window.updateMarqueeSpeed = updateMarqueeSpeed;
window.toggleAll = toggleAll;
window.toggleAllCustomers = toggleAllCustomers;
window.showDocumentPreview = showDocumentPreview;
window.closePreviewModal = closePreviewModal;
window.printPreview = printPreview;
window.makeSearchableDropdown = makeSearchableDropdown;
window.initSearchableDropdowns = initSearchableDropdowns;
window.loadAllData = loadAllData;
window.showPage = showPage;
window.getSafeValue = getSafeValue;
window.formatDate = formatDate;
window.escapeHtml = escapeHtml;
window.addActivityRow = addActivityRow;
window.addQuoteItemRow = addQuoteItemRow;
window.addSaleItemRow = addSaleItemRow;
window.calculateQuoteTotals = calculateQuoteTotals;
window.calculateSaleTotals = calculateSaleTotals;
window.deleteQuoteRow = deleteQuoteRow;
window.renumberQuoteRows = renumberQuoteRows;
window.renumberSaleRows = renumberSaleRows;
window.renumberActivityRows = renumberActivityRows;
window.updateQuoteItemName = updateQuoteItemName;
window.updateSaleItemName = updateSaleItemName;
window.openBasedOnModal = openBasedOnModal;
window.closeBasedOnModal = closeBasedOnModal;
window.selectDocument = selectDocument;
window.getLocation = getLocation;

console.log('✅ تم تحميل النظام المحسن بالكامل وجميع الدوال جاهزة');
  </script>
    
<script>
        (function() {
            document.addEventListener('contextmenu', e => e.preventDefault());
            document.addEventListener('keydown', e => {
                if (e.key === 'F12' || e.keyCode === 123 || 
                    (e.ctrlKey && e.shiftKey && (e.key === 'I' || e.key === 'i' || e.keyCode === 73)) ||
                    (e.ctrlKey && e.shiftKey && (e.key === 'J' || e.key === 'j' || e.keyCode === 74)) ||
                    (e.ctrlKey && (e.key === 'U' || e.key === 'u' || e.keyCode === 85)) ||
                    (e.ctrlKey && e.shiftKey && (e.key === 'C' || e.key === 'c' || e.keyCode === 67)) ||
                    (e.ctrlKey && e.shiftKey && (e.key === 'K' || e.key === 'k' || e.keyCode === 75)) ||
                    (e.ctrlKey && (e.key === 'S' || e.key === 's' || e.keyCode === 83)) ||
                    (e.ctrlKey && (e.key === 'P' || e.key === 'p' || e.keyCode === 80))) {
                    e.preventDefault();
                }
            });
        })();
    </script>

</body>
</html>
