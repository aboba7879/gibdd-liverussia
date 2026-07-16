<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>УГИБДД Live Russia</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
    <style>
        /* ===== БАЗОВЫЕ СТИЛИ (сжаты, но все работают) ===== */
        *{margin:0;padding:0;box-sizing:border-box}
        :root{--primary:#1a3a5c;--primary-light:#2a5f8f;--primary-dark:#0f2640;--accent:#e8a838;--bg:#f0f4fa;--card-bg:#fff;--text:#2c3e50;--text-light:#7a8a9e;--shadow:0 8px 30px rgba(0,0,0,0.08);--radius:12px;--success:#27ae60;--danger:#e74c3c;--warning:#f39c12;--admin-color:#8e44ad;--pingvin-color:#1abc9c;--leader-color:#f39c12}
        body{font-family:'Segoe UI',Tahoma,Geneva,Verdana,sans-serif;background:var(--bg);color:var(--text);line-height:1.6;min-height:100vh}
        .container{max-width:1200px;margin:0 auto;padding:20px}
        .header{background:linear-gradient(135deg,var(--primary-dark),var(--primary-light));color:#fff;padding:20px 30px;border-radius:var(--radius);display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:15px;box-shadow:0 10px 40px rgba(26,58,92,0.25)}
        .header-left{display:flex;align-items:center;gap:15px}
        .header-left .gibdd-emblem{width:60px;height:60px;flex-shrink:0}
        .header-left h1{font-size:2rem;font-weight:700}
        .header-left h1 span{color:var(--accent)}
        .header-left p{opacity:.85;font-size:.95rem}
        .header-right{display:flex;gap:10px;flex-wrap:wrap}
        .header-btn{background:rgba(255,255,255,0.1);border:1px solid rgba(255,255,255,0.2);color:#fff;padding:8px 18px;border-radius:30px;cursor:pointer;font-size:.9rem;display:flex;align-items:center;gap:8px;transition:all .3s}
        .header-btn:hover{background:var(--accent);border-color:var(--accent);transform:translateY(-2px);box-shadow:0 8px 20px rgba(232,168,56,0.3)}
        .nav-bar{background:var(--card-bg);border-radius:var(--radius);padding:0 20px;margin-top:20px;box-shadow:var(--shadow);display:flex;flex-wrap:wrap;justify-content:space-between;align-items:center;position:sticky;top:10px;z-index:100}
        .nav-links{display:flex;list-style:none;gap:5px;flex-wrap:wrap}
        .nav-links li a{display:block;padding:14px 16px;color:var(--text);text-decoration:none;font-weight:500;font-size:.95rem;border-radius:8px;transition:all .3s;cursor:pointer;border:none;background:none}
        .nav-links li a:hover,.nav-links li a.active{background:var(--primary);color:#fff}
        .nav-links li a i{margin-right:8px}
        .nav-search{display:flex;align-items:center;gap:10px}
        .nav-search input{padding:8px 16px;border:2px solid #e8edf3;border-radius:30px;outline:none;font-size:.9rem;background:var(--bg);transition:all .3s}
        .nav-search input:focus{border-color:var(--primary-light);width:200px;background:#fff}
        .nav-search button{background:var(--primary);color:#fff;border:none;padding:8px 16px;border-radius:30px;cursor:pointer;font-weight:600}
        .nav-search button:hover{background:var(--accent)}
        .page{display:none;animation:fadeIn .4s ease}
        .page.active{display:block}
        @keyframes fadeIn{from{opacity:0;transform:translateY(20px)}to{opacity:1;transform:translateY(0)}}
        .main-grid{display:grid;grid-template-columns:2fr 1fr;gap:30px;margin-top:30px}
        @media(max-width:992px){.main-grid{grid-template-columns:1fr}}
        .card{background:var(--card-bg);border-radius:var(--radius);padding:25px;margin-bottom:25px;box-shadow:var(--shadow);border-left:4px solid var(--primary-light);transition:transform .3s,box-shadow .3s}
        .card:hover{transform:translateY(-3px);box-shadow:0 12px 40px rgba(0,0,0,0.12)}
        .card h2{font-size:1.4rem;color:var(--primary);margin-bottom:15px;display:flex;align-items:center;gap:12px;border-bottom:2px solid #eef2f7;padding-bottom:10px}
        .card h2 i{color:var(--accent);font-size:1.4rem}
        .card h3{font-size:1.1rem;color:var(--primary-dark);margin-bottom:8px}
        .auth-form{max-width:450px;margin:0 auto}
        .auth-form .form-group{margin-bottom:18px}
        .auth-form label{display:block;font-weight:600;margin-bottom:5px;color:var(--text)}
        .auth-form input,.auth-form select,.auth-form textarea{width:100%;padding:10px 14px;border:2px solid #e8edf3;border-radius:8px;font-size:1rem;background:var(--bg);transition:all .3s}
        .auth-form input:focus,.auth-form select:focus,.auth-form textarea:focus{border-color:var(--primary-light);outline:none;box-shadow:0 0 0 3px rgba(42,95,143,0.1)}
        .auth-form .btn-primary{width:100%;padding:12px;background:var(--primary);color:#fff;border:none;border-radius:30px;font-size:1.1rem;font-weight:700;cursor:pointer;transition:all .3s}
        .auth-form .btn-primary:hover{background:var(--accent);transform:translateY(-2px)}
        .auth-form .form-footer{text-align:center;margin-top:15px;color:var(--text-light)}
        .auth-form .form-footer a{color:var(--primary);font-weight:600;cursor:pointer;text-decoration:none}
        .auth-form .form-footer a:hover{color:var(--accent)}
        .auth-error{color:var(--danger);font-size:.9rem;margin-top:5px;display:none}
        .auth-success{color:var(--success);font-size:.9rem;margin-top:5px;display:none}
        .profile-card{background:linear-gradient(135deg,var(--primary-dark),var(--primary-light));color:#fff;padding:30px;border-radius:var(--radius);text-align:center}
        .profile-avatar{font-size:3.5rem;background:rgba(255,255,255,0.15);width:90px;height:90px;border-radius:50%;display:flex;align-items:center;justify-content:center;margin:0 auto 15px;border:4px solid var(--accent)}
        .profile-name{font-size:1.6rem;font-weight:700}
        .profile-email{opacity:.8;margin-bottom:15px}
        .role-badge{font-size:.7rem;padding:2px 12px;border-radius:20px;font-weight:600;text-transform:uppercase}
        .role-badge.admin{background:var(--admin-color);color:#fff}
        .role-badge.pingvin{background:var(--pingvin-color);color:#fff}
        .role-badge.leader{background:var(--leader-color);color:#fff}
        .role-badge.user{background:var(--text-light);color:#fff}
        .profile-stats{display:grid;grid-template-columns:repeat(3,1fr);gap:15px;margin-top:20px}
        .profile-stat{background:rgba(255,255,255,0.1);padding:12px;border-radius:10px}
        .profile-stat .number{font-size:1.3rem;font-weight:700}
        .profile-stat .label{font-size:.8rem;opacity:.7}
        .news-meta{display:flex;gap:15px;color:var(--text-light);font-size:.85rem;margin-bottom:10px;flex-wrap:wrap}
        .news-meta span{background:#eef2f7;padding:2px 12px;border-radius:20px;display:inline-flex;align-items:center;gap:6px}
        .news-list .news-item{padding:12px 0;border-bottom:1px solid #eef2f7;cursor:pointer;transition:all .3s}
        .news-list .news-item:last-child{border-bottom:none}
        .news-list .news-item:hover{padding-left:10px;background:#f8fafc}
        .news-item .news-title{font-weight:600;color:var(--primary)}
        .news-item .news-date{font-size:.8rem;color:var(--text-light)}
        .news-item .news-actions{display:flex;gap:8px;margin-top:5px}
        .news-item .news-actions button{padding:3px 12px;border-radius:20px;border:none;cursor:pointer;font-size:.75rem;font-weight:600}
        .news-item .news-actions .edit-btn{background:var(--warning);color:#fff}
        .news-item .news-actions .delete-btn{background:var(--danger);color:#fff}
        .gallery-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:15px;margin:15px 0}
        @media(max-width:600px){.gallery-grid{grid-template-columns:repeat(2,1fr)}}
        .gallery-item{aspect-ratio:1;border-radius:12px;background:linear-gradient(145deg,#e8edf3,#dce3ed);display:flex;flex-direction:column;align-items:center;justify-content:center;font-size:2.2rem;color:var(--text-light);cursor:pointer;transition:all .4s;border:3px solid transparent;position:relative;overflow:hidden}
        .gallery-item:hover{transform:scale(1.05);border-color:var(--accent);box-shadow:0 8px 25px rgba(0,0,0,0.15)}
        .gallery-item .gallery-overlay{position:absolute;bottom:-50px;left:0;right:0;background:rgba(26,58,92,0.85);color:#fff;padding:6px;text-align:center;font-size:.75rem;transition:bottom .3s}
        .gallery-item:hover .gallery-overlay{bottom:0}
        .gallery-item img{width:100%;height:100%;object-fit:cover}
        .gallery-item .gallery-icon{font-size:2.5rem;margin-bottom:5px}
        .photo-preview{max-width:200px;max-height:200px;border-radius:8px;margin-top:10px;display:block}
        .stats-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:15px;margin:15px 0}
        .stat-item{background:linear-gradient(145deg,#f8fafc,#eef2f7);padding:15px;border-radius:12px;text-align:center}
        .stat-number{font-size:2rem;font-weight:800;color:var(--primary)}
        .stat-label{font-size:.85rem;color:var(--text-light);margin-top:4px}
        .schedule-grid{display:grid;grid-template-columns:1fr 1fr;gap:20px}
        @media(max-width:600px){.schedule-grid{grid-template-columns:1fr}}
        .schedule-table{width:100%;border-collapse:collapse;font-size:.9rem}
        .schedule-table th{background:var(--primary);color:#fff;padding:8px 12px;text-align:left;font-weight:600}
        .schedule-table td{padding:8px 12px;border-bottom:1px solid #eef2f7}
        .schedule-note{font-size:.8rem;color:var(--text-light);margin-top:8px;padding:6px 12px;background:#f8fafc;border-radius:8px;display:inline-block}
        .schedule-tabs{display:flex;gap:10px;margin-bottom:20px;flex-wrap:wrap}
        .schedule-tabs button{padding:6px 18px;border:2px solid #e8edf3;background:#fff;border-radius:30px;cursor:pointer;font-weight:600;color:var(--text-light);transition:all .3s}
        .schedule-tabs button.active{background:var(--primary);color:#fff;border-color:var(--primary)}
        .contacts-grid{display:grid;grid-template-columns:1fr 1fr;gap:20px}
        @media(max-width:600px){.contacts-grid{grid-template-columns:1fr}}
        .contact-item{display:flex;align-items:center;gap:15px;padding:12px;background:#f8fafc;border-radius:12px}
        .contact-item i{font-size:1.6rem;color:var(--primary);width:35px;text-align:center}
        .contact-item .contact-label{font-size:.8rem;color:var(--text-light)}
        .contact-item .contact-value{font-weight:600}
        .wanted-tabs,.exam-tabs,.protocol-tabs,.faq-tabs{display:flex;gap:15px;margin-bottom:20px;flex-wrap:wrap}
        .wanted-tabs button,.exam-tabs button,.protocol-tabs button,.faq-tabs button{padding:8px 24px;border:2px solid #e8edf3;background:#fff;border-radius:30px;cursor:pointer;font-weight:600;font-size:1rem;color:var(--text-light);transition:all .3s}
        .wanted-tabs button.active,.exam-tabs button.active,.protocol-tabs button.active,.faq-tabs button.active{background:var(--primary);color:#fff;border-color:var(--primary)}
        .wanted-tabs button:hover,.exam-tabs button:hover,.protocol-tabs button:hover,.faq-tabs button:hover{border-color:var(--primary-light);color:var(--primary)}
        .wanted-tabs button.active:hover,.exam-tabs button.active:hover,.protocol-tabs button.active:hover,.faq-tabs button.active:hover{background:var(--primary-dark);color:#fff}
        .wanted-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:25px;margin-top:20px}
        .wanted-card{background:var(--card-bg);border-radius:var(--radius);overflow:hidden;box-shadow:var(--shadow);transition:transform .3s,box-shadow .3s;border:1px solid #e8edf3}
        .wanted-card:hover{transform:translateY(-5px);box-shadow:0 12px 40px rgba(0,0,0,0.15)}
        .wanted-card .wanted-photo{width:100%;height:200px;background:#e8edf3;display:flex;align-items:center;justify-content:center;font-size:4rem;color:var(--text-light);overflow:hidden}
        .wanted-card .wanted-photo img{width:100%;height:100%;object-fit:cover}
        .wanted-card .wanted-body{padding:18px}
        .wanted-card .wanted-body h3{font-size:1.2rem;margin-bottom:8px;color:var(--primary-dark)}
        .wanted-card .wanted-body .wanted-meta{font-size:.85rem;color:var(--text-light);margin-bottom:8px}
        .wanted-card .wanted-body .wanted-meta i{width:20px}
        .wanted-card .wanted-body .wanted-status{display:inline-block;padding:2px 14px;border-radius:20px;font-size:.8rem;font-weight:600;margin-top:5px}
        .wanted-status.active{background:var(--danger);color:#fff}
        .wanted-status.detained{background:var(--warning);color:#fff}
        .wanted-status.closed{background:var(--success);color:#fff}
        .wanted-card .wanted-actions{margin-top:12px;display:flex;gap:8px;flex-wrap:wrap}
        .wanted-card .wanted-actions button{padding:4px 14px;border:none;border-radius:20px;cursor:pointer;font-size:.8rem;font-weight:600}
        .wanted-card .wanted-actions .edit-btn{background:var(--warning);color:#fff}
        .wanted-card .wanted-actions .delete-btn{background:var(--danger);color:#fff}
        .leadership-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:25px;margin-top:20px}
        .leader-card{background:var(--card-bg);border-radius:var(--radius);overflow:hidden;box-shadow:var(--shadow);transition:transform .3s,box-shadow .3s;border:1px solid #e8edf3;text-align:center;padding:15px}
        .leader-card:hover{transform:translateY(-5px);box-shadow:0 12px 40px rgba(0,0,0,0.15)}
        .leader-card .leader-photo{width:120px;height:120px;border-radius:50%;margin:0 auto 10px;background:#e8edf3;display:flex;align-items:center;justify-content:center;font-size:3rem;color:var(--text-light);overflow:hidden;object-fit:cover}
        .leader-card .leader-photo img{width:100%;height:100%;object-fit:cover}
        .leader-card .leader-name{font-size:1.1rem;font-weight:700;color:var(--primary-dark)}
        .leader-card .leader-position{font-size:.9rem;color:var(--text-light);margin-bottom:8px}
        .leader-card .leader-actions{margin-top:10px;display:flex;gap:8px;justify-content:center;flex-wrap:wrap}
        .leader-card .leader-actions button{padding:4px 14px;border:none;border-radius:20px;cursor:pointer;font-size:.8rem;font-weight:600}
        .leader-card .leader-actions .edit-btn{background:var(--warning);color:#fff}
        .leader-card .leader-actions .delete-btn{background:var(--danger);color:#fff}
        .protocol-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));gap:25px;margin-top:20px}
        .protocol-card{background:var(--card-bg);border-radius:var(--radius);overflow:hidden;box-shadow:var(--shadow);transition:transform .3s,box-shadow .3s;border:1px solid #e8edf3}
        .protocol-card:hover{transform:translateY(-5px);box-shadow:0 12px 40px rgba(0,0,0,0.15)}
        .protocol-card .protocol-header{padding:12px 18px;background:var(--primary-light);color:#fff;display:flex;justify-content:space-between;align-items:center}
        .protocol-card .protocol-body{padding:18px}
        .protocol-card .protocol-body .protocol-meta{font-size:.9rem;color:var(--text-light);margin-bottom:5px}
        .protocol-card .protocol-body .protocol-meta i{width:20px}
        .protocol-card .protocol-status{display:inline-block;padding:2px 12px;border-radius:20px;font-size:.8rem;font-weight:600}
        .protocol-status.active{background:var(--danger);color:#fff}
        .protocol-status.pending{background:var(--warning);color:#fff}
        .protocol-status.closed{background:var(--success);color:#fff}
        .protocol-card .protocol-actions{margin-top:12px;display:flex;gap:8px;flex-wrap:wrap}
        .protocol-card .protocol-actions button{padding:4px 14px;border:none;border-radius:20px;cursor:pointer;font-size:.8rem;font-weight:600}
        .protocol-card .protocol-actions .edit-btn{background:var(--warning);color:#fff}
        .protocol-card .protocol-actions .delete-btn{background:var(--danger);color:#fff}
        .faq-grid{display:grid;grid-template-columns:1fr;gap:20px;margin-top:20px}
        .faq-item{background:var(--card-bg);border-radius:var(--radius);padding:18px;box-shadow:var(--shadow);border-left:4px solid var(--primary-light)}
        .faq-item .faq-question{font-weight:600;color:var(--primary-dark)}
        .faq-item .faq-meta{font-size:.8rem;color:var(--text-light);margin:5px 0}
        .faq-item .faq-answer{background:#f8fafc;padding:10px;border-radius:8px;margin-top:10px;border-left:3px solid var(--success)}
        .faq-item .faq-actions{margin-top:10px;display:flex;gap:8px;flex-wrap:wrap}
        .faq-item .faq-actions button{padding:4px 14px;border:none;border-radius:20px;cursor:pointer;font-size:.8rem;font-weight:600}
        .faq-item .faq-actions .answer-btn{background:var(--success);color:#fff}
        .faq-item .faq-actions .delete-btn{background:var(--danger);color:#fff}
        .footer{background:var(--primary-dark);color:#c0d0e0;border-radius:var(--radius);padding:25px;margin-top:40px;display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:20px}
        .footer h4{color:#fff;margin-bottom:10px;font-size:1rem}
        .footer ul{list-style:none;padding:0}
        .footer ul li{margin-bottom:6px}
        .footer ul li a{color:#a0b0c4;text-decoration:none;transition:all .3s;cursor:pointer}
        .footer ul li a:hover{color:var(--accent)}
        .footer-bottom{grid-column:1/-1;text-align:center;padding-top:15px;border-top:1px solid rgba(255,255,255,0.06);font-size:.85rem;opacity:.7}
        .footer-bottom strong{color:#fff}
        .modal{display:none;position:fixed;top:0;left:0;right:0;bottom:0;background:rgba(0,0,0,0.6);backdrop-filter:blur(6px);z-index:1000;align-items:center;justify-content:center}
        .modal.active{display:flex}
        .modal-content{background:var(--card-bg);max-width:650px;width:90%;padding:30px;border-radius:var(--radius);box-shadow:0 30px 60px rgba(0,0,0,0.3);position:relative;max-height:90vh;overflow-y:auto}
        .modal-content .close-btn{position:absolute;top:10px;right:15px;font-size:1.6rem;cursor:pointer;color:var(--text-light);background:none;border:none}
        .modal-content .close-btn:hover{color:var(--danger);transform:rotate(90deg)}
        .btn-admin{background:var(--admin-color);color:#fff;border:none;padding:8px 20px;border-radius:30px;cursor:pointer;font-weight:600;transition:all .3s}
        .btn-admin:hover{opacity:.85;transform:translateY(-2px)}
        .btn-pingvin{background:var(--pingvin-color);color:#fff;border:none;padding:8px 20px;border-radius:30px;cursor:pointer;font-weight:600;transition:all .3s}
        .btn-pingvin:hover{opacity:.85;transform:translateY(-2px)}
        .btn-leader{background:var(--leader-color);color:#fff;border:none;padding:8px 20px;border-radius:30px;cursor:pointer;font-weight:600;transition:all .3s}
        .btn-leader:hover{opacity:.85;transform:translateY(-2px)}
        .btn-secondary{background:var(--danger);color:#fff;border:none;padding:8px 18px;border-radius:30px;cursor:pointer;font-weight:600;transition:all .3s}
        .btn-secondary:hover{opacity:.8;transform:translateY(-2px)}
        .btn-sm{padding:4px 12px;font-size:.8rem}
        .flex-between{display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:10px}
        .text-muted{color:var(--text-light)}
        .text-center{text-align:center}
        .mt-10{margin-top:10px}
        .mt-20{margin-top:20px}
        .toast{position:fixed;bottom:30px;right:30px;background:var(--primary-dark);color:#fff;padding:14px 22px;border-radius:12px;box-shadow:0 10px 40px rgba(0,0,0,0.2);z-index:2000;transform:translateY(100px);opacity:0;transition:all .5s;max-width:400px}
        .toast.show{transform:translateY(0);opacity:1}
        .toast.success{background:var(--success)}
        .toast.error{background:var(--danger)}
        .toast.info{background:var(--primary)}
        .question-card{background:#f8fafc;padding:15px;border-radius:8px;margin-bottom:15px;border-left:4px solid var(--primary-light)}
        .question-card .q-text{font-weight:600;margin-bottom:8px}
        .question-card .q-options{padding-left:20px}
        .question-card .q-options label{display:block;margin:5px 0;cursor:pointer}
        .question-card .q-options input[type="radio"]{margin-right:8px}
        .exam-result{font-size:1.2rem;font-weight:700;padding:15px;border-radius:8px;text-align:center}
        .exam-result.success{background:var(--success);color:#fff}
        .exam-result.fail{background:var(--danger);color:#fff}
        .ticket-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(200px,1fr));gap:15px}
        .ticket-card{background:var(--card-bg);padding:15px;border-radius:var(--radius);box-shadow:var(--shadow);text-align:center;cursor:pointer;transition:all .3s;border:2px solid transparent}
        .ticket-card:hover{transform:translateY(-3px);border-color:var(--accent)}
        .ticket-card .ticket-number{font-size:2rem;font-weight:700;color:var(--primary)}
        .ticket-card .ticket-info{font-size:.85rem;color:var(--text-light)}
        .question-edit-item{background:#f8fafc;padding:12px;border-radius:8px;margin-bottom:10px;border-left:4px solid var(--warning)}
        @media(max-width:768px){
            .header{flex-direction:column;text-align:center;padding:15px}
            .header-left{flex-direction:column}
            .header-left h1{font-size:1.6rem}
            .nav-bar{flex-direction:column;padding:10px;top:0}
            .nav-links{justify-content:center}
            .nav-links li a{padding:8px 12px;font-size:.85rem}
            .nav-search{width:100%;margin-top:10px;justify-content:center}
            .card{padding:18px}
            .footer{grid-template-columns:1fr;text-align:center}
            .wanted-grid,.leadership-grid,.ticket-grid,.protocol-grid,.faq-grid{grid-template-columns:1fr}
            .gallery-grid{grid-template-columns:repeat(2,1fr)}
        }
    </style>
</head>
<body>
<div class="container">

    <!-- ШАПКА С ГЕРБОМ -->
    <header class="header">
        <div class="header-left">
            <div class="gibdd-emblem">
                <svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
                    <rect x="5" y="5" width="90" height="90" rx="10" ry="10" fill="#1a3a5c" stroke="#e8a838" stroke-width="3"/>
                    <rect x="25" y="25" width="50" height="50" fill="white" rx="3"/>
                    <line x1="25" y1="50" x2="75" y2="50" stroke="#e8a838" stroke-width="4" stroke-dasharray="6 4"/>
                    <g transform="translate(50, 25) rotate(45)">
                        <rect x="-4" y="0" width="8" height="40" fill="#e74c3c" rx="2"/>
                        <rect x="-4" y="8" width="8" height="6" fill="white"/>
                        <rect x="-4" y="20" width="8" height="6" fill="white"/>
                        <rect x="-4" y="32" width="8" height="6" fill="white"/>
                        <rect x="-6" y="40" width="12" height="8" fill="#2c3e50" rx="2"/>
                    </g>
                    <polygon points="50,30 56,45 72,45 59,55 64,70 50,62 36,70 41,55 28,45 44,45" fill="#e8a838" stroke="white" stroke-width="1"/>
                </svg>
            </div>
            <div>
                <h1>УГИБДД <span>Live Russia</span></h1>
                <p><i class="fas fa-shield-alt"></i> Официальный портал Госавтоинспекции</p>
            </div>
        </div>
        <div class="header-right">
            <button class="header-btn" onclick="openModal('hotline')"><i class="fas fa-phone"></i> Телефон доверия</button>
            <button class="header-btn" onclick="toggleTheme()"><i class="fas fa-moon"></i> Тема</button>
            <button class="header-btn" id="authBtn" onclick="navigateTo('profile')"><i class="fas fa-user-circle"></i> <span id="authBtnText">Войти</span></button>
        </div>
    </header>

    <!-- НАВИГАЦИЯ -->
    <nav class="nav-bar">
        <ul class="nav-links">
            <li><a class="active" onclick="navigateTo('home')" data-page="home"><i class="fas fa-home"></i> Главная</a></li>
            <li><a onclick="navigateTo('news')" data-page="news"><i class="fas fa-newspaper"></i> Новости</a></li>
            <li><a onclick="navigateTo('schedule')" data-page="schedule"><i class="fas fa-calendar-alt"></i> Расписание</a></li>
            <li><a onclick="navigateTo('gallery')" data-page="gallery"><i class="fas fa-images"></i> Галерея</a></li>
            <li><a onclick="navigateTo('stats')" data-page="stats"><i class="fas fa-chart-bar"></i> Статистика</a></li>
            <li><a onclick="navigateTo('wanted')" data-page="wanted"><i class="fas fa-search"></i> Розыск</a></li>
            <li><a onclick="navigateTo('protocols')" data-page="protocols"><i class="fas fa-file-alt"></i> Протоколы</a></li>
            <li><a onclick="navigateTo('faq')" data-page="faq"><i class="fas fa-question-circle"></i> Вопрос-ответ</a></li>
            <li><a onclick="navigateTo('leadership')" data-page="leadership"><i class="fas fa-user-tie"></i> Руководство</a></li>
            <li><a onclick="navigateTo('contacts')" data-page="contacts"><i class="fas fa-phone-alt"></i> Контакты</a></li>
            <li id="examNavLink" style="display:none;"><a onclick="navigateTo('exams')" data-page="exams"><i class="fas fa-graduation-cap"></i> Экзамены</a></li>
            <li><a onclick="navigateTo('profile')" data-page="profile"><i class="fas fa-user"></i> Личный кабинет</a></li>
            <li id="adminNavLink" style="display:none;"><a onclick="navigateTo('admin')" data-page="admin"><i class="fas fa-user-shield"></i> Админ-панель</a></li>
        </ul>
        <div class="nav-search">
            <input type="text" placeholder="Поиск..." id="searchInput">
            <button onclick="searchSite()"><i class="fas fa-search"></i></button>
        </div>
    </nav>

    <!-- СТРАНИЦЫ -->

    <!-- ГЛАВНАЯ -->
    <div class="page active" id="page-home">
        <div class="main-grid">
            <div class="left-col">
                <section class="card"><h2><i class="fas fa-bolt"></i> ПОСЛЕДНЯЯ НОВОСТЬ</h2><div id="homeNewsContent"></div></section>
                <section class="card"><h2><i class="fas fa-clock"></i> Режим работы МРЭО</h2>
                    <div class="schedule-grid">
                        <div><table class="schedule-table"><thead><tr><th>ДЕНЬ НЕДЕЛИ</th><th>ВРЕМЯ РАБОТЫ</th></tr></thead>
                        <tbody><tr><td>ВТОРНИК</td><td>17.30 - 19.00</td></tr><tr><td>СРЕДА</td><td>17.30 - 19.00</td></tr><tr><td>ЧЕТВЕРГ</td><td>19.00 - 20.00</td></tr><tr><td>ПЯТНИЦА</td><td>19.00 - 20.00</td></tr><tr><td>СУББОТА</td><td>17.30 - 19.00</td></tr></tbody></table>
                        <div class="schedule-note"><i class="fas fa-times-circle" style="color:var(--danger);"></i> ВОСКРЕСЕНЬЕ, ПОНЕДЕЛЬНИК — НЕ ПРИЕМНЫЙ ДЕНЬ</div></div>
                        <div><table class="schedule-table"><thead><tr><th>ДЕНЬ НЕДЕЛИ</th><th>ВРЕМЯ РАБОТЫ</th></tr></thead>
                        <tbody><tr><td>ВТОРНИК</td><td>15.00 - 18.00</td></tr><tr><td>СРЕДА</td><td>12.00 - 15.00</td></tr><tr><td>ЧЕТВЕРГ</td><td>17.00 - 20.00</td></tr><tr><td>ПЯТНИЦА</td><td>15.00 - 18.00</td></tr><tr><td>СУББОТА</td><td>16.00 - 19.00</td></tr></tbody></table>
                        <div class="schedule-note"><i class="fas fa-check-circle" style="color:var(--success);"></i> (прием по живой очереди)</div>
                        <div class="schedule-note"><i class="fas fa-times-circle" style="color:var(--danger);"></i> ВОСКРЕСЕНЬЕ, ПОНЕДЕЛЬНИК — НЕ ПРИЕМНЫЙ ДЕНЬ</div></div>
                    </div>
                </section>
            </div>
            <div class="sidebar">
                <section class="card" style="border-left-color:var(--accent);">
                    <h2><i class="fas fa-phone-alt"></i> Телефон доверия</h2>
                    <div style="text-align:center;padding:15px;background:#f8fafc;border-radius:12px;">
                        <i class="fas fa-headset" style="font-size:2.2rem;color:var(--primary);"></i>
                        <h3 style="font-size:1.6rem;color:var(--primary);" id="homePhone">8-800-200-00-00</h3>
                        <p class="text-muted"><i class="fas fa-clock"></i> Круглосуточно, анонимно</p>
                    </div>
                </section>
                <section class="card"><h2><i class="fas fa-chart-line"></i> Аварийность</h2><p class="text-muted">На 11.07.2026</p>
                    <div class="stats-grid">
                        <div class="stat-item"><div class="stat-number" id="homeStatDtp">249</div><div class="stat-label">ДТП</div></div>
                        <div class="stat-item"><div class="stat-number" id="homeStatInjured">54</div><div class="stat-label">Пострадавших</div></div>
                        <div class="stat-item"><div class="stat-number" id="homeStatDead">19</div><div class="stat-label">Погибло</div></div>
                    </div>
                </section>
                <section class="card"><h2><i class="fas fa-link"></i> Быстрые ссылки</h2>
                    <ul style="list-style:none;padding:0;">
                        <li style="padding:8px 0;border-bottom:1px solid #eef2f7;"><a href="#" style="color:var(--text);text-decoration:none;"><i class="fas fa-gavel" style="color:var(--accent);"></i> Проверка штрафов</a></li>
                        <li style="padding:8px 0;border-bottom:1px solid #eef2f7;"><a href="#" style="color:var(--text);text-decoration:none;"><i class="fas fa-calendar-check" style="color:var(--accent);"></i> Запись на прием</a></li>
                        <li style="padding:8px 0;"><a href="#" style="color:var(--text);text-decoration:none;"><i class="fas fa-id-card" style="color:var(--accent);"></i> Госуслуги</a></li>
                    </ul>
                </section>
            </div>
        </div>
    </div>

    <!-- НОВОСТИ -->
    <div class="page" id="page-news">
        <section class="card">
            <div class="flex-between"><h2><i class="fas fa-newspaper"></i> Все новости</h2><button id="addNewsBtn" class="btn-admin" style="display:none;" onclick="openModal('addNews')"><i class="fas fa-plus"></i> Добавить новость</button></div>
            <div class="news-list" id="newsList"></div>
        </section>
    </div>

    <!-- РАСПИСАНИЕ -->
    <div class="page" id="page-schedule">
        <section class="card">
            <h2><i class="fas fa-calendar-alt"></i> Полное расписание</h2>
            <div class="schedule-tabs">
                <button class="active" onclick="switchSchedule('first', this)">Основной график</button>
                <button onclick="switchSchedule('second', this)">Живая очередь</button>
                <button onclick="switchSchedule('third', this)">Экзамены</button>
            </div>
            <div id="scheduleFirst" class="schedule-grid"><div><table class="schedule-table"><thead><tr><th>ДЕНЬ</th><th>ВРЕМЯ</th></tr></thead><tbody><tr><td>ВТОРНИК</td><td>17.30 - 19.00</td></tr><tr><td>СРЕДА</td><td>17.30 - 19.00</td></tr><tr><td>ЧЕТВЕРГ</td><td>19.00 - 20.00</td></tr><tr><td>ПЯТНИЦА</td><td>19.00 - 20.00</td></tr><tr><td>СУББОТА</td><td>17.30 - 19.00</td></tr></tbody></table><div class="schedule-note">ВС, ПН — выходной</div></div><div><table class="schedule-table"><thead><tr><th>ДЕНЬ</th><th>ВРЕМЯ</th></tr></thead><tbody><tr><td>ВТОРНИК</td><td>15.00 - 18.00</td></tr><tr><td>СРЕДА</td><td>12.00 - 15.00</td></tr><tr><td>ЧЕТВЕРГ</td><td>17.00 - 20.00</td></tr><tr><td>ПЯТНИЦА</td><td>15.00 - 18.00</td></tr><tr><td>СУББОТА</td><td>16.00 - 19.00</td></tr></tbody></table><div class="schedule-note">Живая очередь</div></div></div>
            <div id="scheduleSecond" class="schedule-grid" style="display:none;"><div><table class="schedule-table"><thead><tr><th>ДЕНЬ</th><th>ВРЕМЯ</th></tr></thead><tbody><tr><td>ВТОРНИК</td><td>10.00 - 13.00</td></tr><tr><td>СРЕДА</td><td>14.00 - 17.00</td></tr><tr><td>ЧЕТВЕРГ</td><td>10.00 - 13.00</td></tr><tr><td>ПЯТНИЦА</td><td>14.00 - 17.00</td></tr><tr><td>СУББОТА</td><td>10.00 - 14.00</td></tr></tbody></table><div class="schedule-note">Дополнительные часы</div></div><div><table class="schedule-table"><thead><tr><th>ДЕНЬ</th><th>ВРЕМЯ</th></tr></thead><tbody><tr><td>ВТОРНИК</td><td>08.00 - 12.00</td></tr><tr><td>СРЕДА</td><td>08.00 - 12.00</td></tr><tr><td>ЧЕТВЕРГ</td><td>08.00 - 12.00</td></tr><tr><td>ПЯТНИЦА</td><td>08.00 - 12.00</td></tr><tr><td>СУББОТА</td><td>08.00 - 11.00</td></tr></tbody></table><div class="schedule-note">Утренние часы</div></div></div>
            <div id="scheduleThird" class="schedule-grid" style="display:none;"><div><table class="schedule-table"><thead><tr><th>ДЕНЬ</th><th>ВРЕМЯ</th></tr></thead><tbody><tr><td>ПОНЕДЕЛЬНИК</td><td>09.00 - 13.00</td></tr><tr><td>СРЕДА</td><td>09.00 - 13.00</td></tr><tr><td>ПЯТНИЦА</td><td>09.00 - 13.00</td></tr></tbody></table><div class="schedule-note">Теоретический экзамен</div></div><div><table class="schedule-table"><thead><tr><th>ДЕНЬ</th><th>ВРЕМЯ</th></tr></thead><tbody><tr><td>ВТОРНИК</td><td>10.00 - 16.00</td></tr><tr><td>ЧЕТВЕРГ</td><td>10.00 - 16.00</td></tr><tr><td>СУББОТА</td><td>10.00 - 14.00</td></tr></tbody></table><div class="schedule-note">Практический экзамен</div></div></div>
        </section>
    </div>

    <!-- ГАЛЕРЕЯ -->
    <div class="page" id="page-gallery">
        <section class="card">
            <div class="flex-between"><h2><i class="fas fa-images"></i> Галерея</h2><button id="addGalleryBtn" class="btn-admin" style="display:none;" onclick="openModal('addGallery')"><i class="fas fa-plus"></i> Добавить фото</button></div>
            <div class="gallery-grid" id="galleryGrid"></div>
            <p class="text-center text-muted"><i class="fas fa-info-circle"></i> Кликните на изображение для увеличения</p>
        </section>
    </div>

    <!-- СТАТИСТИКА -->
    <div class="page" id="page-stats">
        <section class="card">
            <div class="flex-between"><h2><i class="fas fa-chart-bar"></i> Статистика аварийности</h2><button id="editStatsBtn" class="btn-admin" style="display:none;" onclick="openModal('editStats')"><i class="fas fa-edit"></i> Редактировать</button></div>
            <p class="text-muted">Данные на <span id="statsDate">11.07.2026</span></p>
            <div class="stats-grid" style="margin-top:15px;">
                <div class="stat-item" style="border:2px solid var(--danger);"><div class="stat-number" id="statDtp">249</div><div class="stat-label"><i class="fas fa-car-crash"></i> Всего ДТП</div></div>
                <div class="stat-item" style="border:2px solid var(--warning);"><div class="stat-number" id="statInjured">54</div><div class="stat-label"><i class="fas fa-user-injured"></i> Пострадавших</div></div>
                <div class="stat-item" style="border:2px solid var(--danger);"><div class="stat-number" id="statDead">19</div><div class="stat-label"><i class="fas fa-skull"></i> Погибших</div></div>
            </div>
        </section>
    </div>

    <!-- РОЗЫСК -->
    <div class="page" id="page-wanted">
        <section class="card">
            <h2><i class="fas fa-search"></i> Розыск</h2>
            <div class="wanted-tabs">
                <button class="active" onclick="switchWantedTab('persons', this)"><i class="fas fa-user"></i> Лица</button>
                <button onclick="switchWantedTab('cars', this)"><i class="fas fa-car"></i> Автомобили</button>
            </div>
            <div id="wantedPersonsSection">
                <div class="flex-between"><h3 style="border:none;padding:0;margin:0;">Лица в розыске</h3><button id="addWantedBtn" class="btn-admin" style="display:none;" onclick="openModal('addWanted')"><i class="fas fa-plus"></i> Добавить</button></div>
                <div id="wantedPersonsList" class="wanted-grid"></div>
            </div>
            <div id="wantedCarsSection" style="display:none;">
                <div class="flex-between"><h3 style="border:none;padding:0;margin:0;">Автомобили в розыске</h3><button id="addWantedCarBtn" class="btn-admin" style="display:none;" onclick="openModal('addWantedCar')"><i class="fas fa-plus"></i> Добавить авто</button></div>
                <div id="wantedCarsList" class="wanted-grid"></div>
            </div>
        </section>
    </div>

    <!-- ПРОТОКОЛЫ -->
    <div class="page" id="page-protocols">
        <section class="card">
            <h2><i class="fas fa-file-alt"></i> Протоколы и требования</h2>
            <div class="protocol-tabs">
                <button class="active" onclick="switchProtocolTab('all', this)"><i class="fas fa-list"></i> Все</button>
                <button onclick="switchProtocolTab('protocol', this)"><i class="fas fa-gavel"></i> Протоколы</button>
                <button onclick="switchProtocolTab('requirement', this)"><i class="fas fa-file-signature"></i> Требования</button>
            </div>
            <div class="flex-between">
                <p class="text-muted" id="protocolStatusMsg">Список документов</p>
                <button id="addProtocolBtn" class="btn-pingvin" style="display:none;" onclick="openModal('addProtocol')">
                    <i class="fas fa-plus"></i> Создать документ
                </button>
            </div>
            <div id="protocolList" class="protocol-grid mt-10"></div>
        </section>
    </div>

    <!-- ВОПРОС-ОТВЕТ (FAQ) -->
    <div class="page" id="page-faq">
        <section class="card">
            <h2><i class="fas fa-question-circle"></i> Вопрос-ответ</h2>
            <div class="faq-tabs">
                <button class="active" onclick="switchFaqTab('ask', this)"><i class="fas fa-pencil-alt"></i> Задать вопрос</button>
                <button onclick="switchFaqTab('manage', this)" id="faqManageTab" style="display:none;"><i class="fas fa-list"></i> Управление вопросами</button>
            </div>
            <!-- Вкладка "Задать вопрос" -->
            <div id="faqAskSection">
                <p class="text-muted">Задайте вопрос руководству организации. Ответ будет отправлен в ваш личный кабинет.</p>
                <form id="askForm" class="auth-form" style="max-width:100%;">
                    <div class="form-group">
                        <label>Тема вопроса</label>
                        <input type="text" id="faqSubject" placeholder="Кратко опишите суть" required>
                    </div>
                    <div class="form-group">
                        <label>Ваш вопрос</label>
                        <textarea id="faqMessage" rows="4" placeholder="Подробно изложите вопрос..." required></textarea>
                    </div>
                    <button type="submit" class="btn-primary" onclick="submitQuestion(event)"><i class="fas fa-paper-plane"></i> Отправить вопрос</button>
                </form>
                <div id="userQuestions" class="mt-20"></div>
            </div>
            <!-- Вкладка "Управление вопросами" (только для лидера) -->
            <div id="faqManageSection" style="display:none;">
                <div class="flex-between">
                    <p class="text-muted">Вопросы от пользователей</p>
                </div>
                <div id="faqManageList" class="faq-grid mt-10"></div>
            </div>
        </section>
    </div>

    <!-- РУКОВОДСТВО -->
    <div class="page" id="page-leadership">
        <section class="card">
            <div class="flex-between"><h2><i class="fas fa-user-tie"></i> Руководство</h2><button id="addLeaderBtn" class="btn-admin" style="display:none;" onclick="openModal('addLeadership')"><i class="fas fa-plus"></i> Добавить руководителя</button></div>
            <p class="text-muted">Информация о руководящем составе</p>
            <div id="leadershipList" class="leadership-grid"></div>
        </section>
    </div>

    <!-- КОНТАКТЫ -->
    <div class="page" id="page-contacts">
        <section class="card">
            <div class="flex-between"><h2><i class="fas fa-address-book"></i> Контакты</h2><button id="editContactsBtn" class="btn-admin" style="display:none;" onclick="openModal('editContacts')"><i class="fas fa-edit"></i> Редактировать контакты</button></div>
            <div class="contacts-grid" id="contactsContainer"></div>
        </section>
    </div>

    <!-- ЭКЗАМЕНЫ -->
    <div class="page" id="page-exams">
        <section class="card">
            <h2><i class="fas fa-graduation-cap"></i> Экзамены</h2>
            <div class="exam-tabs">
                <button class="active" onclick="switchExamTab('tickets', this)"><i class="fas fa-ticket-alt"></i> Билеты</button>
                <button onclick="switchExamTab('questions', this)" id="examQuestionsTab" style="display:none;"><i class="fas fa-list"></i> Вопросы</button>
            </div>
            <div id="examTicketsSection">
                <div class="flex-between"><p class="text-muted">Выберите билет для прохождения экзамена</p><button id="createTicketBtn" class="btn-admin" style="display:none;" onclick="createTicket()"><i class="fas fa-plus"></i> Создать билет</button></div>
                <div id="ticketsList" class="ticket-grid mt-10"></div>
            </div>
            <div id="examQuestionsSection" style="display:none;">
                <div class="flex-between"><p class="text-muted">Управление вопросами</p><button class="btn-admin" onclick="openModal('addQuestion')"><i class="fas fa-plus"></i> Добавить вопрос</button></div>
                <div id="questionsList" class="mt-10"></div>
            </div>
        </section>
    </div>

    <!-- АДМИН-ПАНЕЛЬ -->
    <div class="page" id="page-admin">
        <section class="card" style="border-left-color:var(--admin-color);">
            <h2><i class="fas fa-user-shield" style="color:var(--admin-color);"></i> Административная панель</h2>
            <p class="text-muted">Управление контентом и пользователями</p>
            <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:15px;margin-top:20px;">
                <div style="background:#f8fafc;padding:15px;border-radius:12px;text-align:center;cursor:pointer;" onclick="navigateTo('news')"><i class="fas fa-newspaper" style="font-size:1.8rem;color:var(--primary);"></i><h4>Новости</h4></div>
                <div style="background:#f8fafc;padding:15px;border-radius:12px;text-align:center;cursor:pointer;" onclick="navigateTo('gallery')"><i class="fas fa-images" style="font-size:1.8rem;color:var(--primary);"></i><h4>Галерея</h4></div>
                <div style="background:#f8fafc;padding:15px;border-radius:12px;text-align:center;cursor:pointer;" onclick="navigateTo('stats')"><i class="fas fa-chart-bar" style="font-size:1.8rem;color:var(--primary);"></i><h4>Статистика</h4></div>
                <div style="background:#f8fafc;padding:15px;border-radius:12px;text-align:center;cursor:pointer;" onclick="navigateTo('wanted')"><i class="fas fa-search" style="font-size:1.8rem;color:var(--primary);"></i><h4>Розыск</h4></div>
                <div style="background:#f8fafc;padding:15px;border-radius:12px;text-align:center;cursor:pointer;" onclick="navigateTo('protocols')"><i class="fas fa-file-alt" style="font-size:1.8rem;color:var(--primary);"></i><h4>Протоколы</h4></div>
                <div style="background:#f8fafc;padding:15px;border-radius:12px;text-align:center;cursor:pointer;" onclick="navigateTo('faq')"><i class="fas fa-question-circle" style="font-size:1.8rem;color:var(--primary);"></i><h4>Вопрос-ответ</h4></div>
                <div style="background:#f8fafc;padding:15px;border-radius:12px;text-align:center;cursor:pointer;" onclick="navigateTo('leadership')"><i class="fas fa-user-tie" style="font-size:1.8rem;color:var(--primary);"></i><h4>Руководство</h4></div>
                <div style="background:#f8fafc;padding:15px;border-radius:12px;text-align:center;cursor:pointer;" onclick="navigateTo('contacts')"><i class="fas fa-phone-alt" style="font-size:1.8rem;color:var(--primary);"></i><h4>Контакты</h4></div>
                <div style="background:#f8fafc;padding:15px;border-radius:12px;text-align:center;cursor:pointer;" onclick="navigateTo('exams')"><i class="fas fa-graduation-cap" style="font-size:1.8rem;color:var(--primary);"></i><h4>Экзамены</h4></div>
                <div style="background:#f8fafc;padding:15px;border-radius:12px;text-align:center;cursor:pointer;" onclick="openModal('manageUsers')"><i class="fas fa-users" style="font-size:1.8rem;color:var(--primary);"></i><h4>Пользователи</h4></div>
            </div>
            <div style="margin-top:20px;padding:15px;background:#f8fafc;border-radius:12px;">
                <p>Всего пользователей: <strong id="totalUsersCount">0</strong></p>
                <p>Новостей: <strong id="totalNewsCount">0</strong></p>
                <p>В розыске (лиц): <strong id="totalWantedCount">0</strong></p>
                <p>В розыске (авто): <strong id="totalWantedCarsCount">0</strong></p>
                <p>Руководителей: <strong id="totalLeadershipCount">0</strong></p>
                <p>Вопросов: <strong id="totalQuestionsCount">0</strong></p>
                <p>Билетов: <strong id="totalTicketsCount">0</strong></p>
                <p>Изображений: <strong id="totalGalleryCount">0</strong></p>
                <p>Протоколов/требований: <strong id="totalProtocolsCount">0</strong></p>
                <p>Вопросов в FAQ: <strong id="totalFaqCount">0</strong></p>
            </div>
        </section>
    </div>

    <!-- ЛИЧНЫЙ КАБИНЕТ -->
    <div class="page" id="page-profile">
        <div id="profileContent"></div>
    </div>

    <!-- ФУТЕР -->
    <footer class="footer">
        <div>
            <h4><i class="fas fa-car-side"></i> УГИБДД Live Russia</h4>
            <p style="opacity:0.8;font-size:0.9rem;">Официальный портал Госавтоинспекции</p>
        </div>
        <div>
            <h4>Разделы</h4>
            <ul>
                <li><a onclick="navigateTo('home')"><i class="fas fa-chevron-right"></i> Главная</a></li>
                <li><a onclick="navigateTo('news')"><i class="fas fa-chevron-right"></i> Новости</a></li>
                <li><a onclick="navigateTo('wanted')"><i class="fas fa-chevron-right"></i> Розыск</a></li>
                <li><a onclick="navigateTo('protocols')"><i class="fas fa-chevron-right"></i> Протоколы</a></li>
                <li><a onclick="navigateTo('faq')"><i class="fas fa-chevron-right"></i> Вопрос-ответ</a></li>
                <li id="footerExamLink" style="display:none;"><a onclick="navigateTo('exams')"><i class="fas fa-chevron-right"></i> Экзамены</a></li>
            </ul>
        </div>
        <div>
            <h4>Полезное</h4>
            <ul>
                <li><a href="#"><i class="fas fa-chevron-right"></i> Вопрос-ответ</a></li>
                <li><a href="#"><i class="fas fa-chevron-right"></i> Памятка водителя</a></li>
            </ul>
        </div>
        <div>
            <h4>Контакты</h4>
            <ul>
                <li><i class="fas fa-phone"></i> <span id="footerPhone">8-800-200-00-00</span></li>
                <li><i class="fas fa-envelope"></i> <span id="footerEmail">info@live-russia.ru</span></li>
                <li><i class="fas fa-map-marker-alt"></i> <span id="footerAddress">г. Южный, ул. Соколовского, д. 67</span></li>
            </ul>
        </div>
        <div class="footer-bottom">
            <p>© 2026 <strong>Live Russia</strong> — Все права защищены.</p>
            <p style="margin-top:4px;opacity:0.6;font-size:0.8rem;"><i class="fas fa-shield-alt"></i> Сайт не является официальным ресурсом ведомства.</p>
        </div>
    </footer>
</div>

<!-- МОДАЛЬНОЕ ОКНО -->
<div class="modal" id="mainModal">
    <div class="modal-content">
        <button class="close-btn" onclick="closeModal()"><i class="fas fa-times"></i></button>
        <div id="modalBody"></div>
    </div>
</div>

<!-- TOAST -->
<div class="toast" id="toast"></div>

<script>
// ============================================================
// 1. ГЛОБАЛЬНЫЕ ДАННЫЕ
// ============================================================

let currentUser = null;
let users = [];
let newsData = [];
let galleryData = [];
let wantedData = [];
let wantedCarsData = [];
let leadershipData = [];
let contactsData = { phone: '8-800-200-00-00', email: 'info@live-russia.ru', address: 'г. Южный, ул. Соколовского, д. 67', workHours: 'Пн-Пт: 09:00 - 18:00' };
let statsData = { dtp: 249, injured: 54, dead: 19, date: '11.07.2026' };
let questionsData = [];
let ticketsData = [];
let protocolsData = [];
let faqData = []; // {id, userId, subject, message, answer, date, answered}

// ============================================================
// 2. ЗАГРУЗКА/СОХРАНЕНИЕ ДАННЫХ
// ============================================================

function loadAllData() {
    try {
        users = JSON.parse(localStorage.getItem('live_russia_users')) || [];
        newsData = JSON.parse(localStorage.getItem('live_russia_news')) || getDefaultNews();
        galleryData = JSON.parse(localStorage.getItem('live_russia_gallery')) || [];
        wantedData = JSON.parse(localStorage.getItem('live_russia_wanted')) || getDefaultWanted();
        wantedCarsData = JSON.parse(localStorage.getItem('live_russia_wanted_cars')) || getDefaultWantedCars();
        leadershipData = JSON.parse(localStorage.getItem('live_russia_leadership')) || getDefaultLeadership();
        if (localStorage.getItem('live_russia_contacts')) contactsData = JSON.parse(localStorage.getItem('live_russia_contacts'));
        if (localStorage.getItem('live_russia_stats')) statsData = JSON.parse(localStorage.getItem('live_russia_stats'));
        questionsData = JSON.parse(localStorage.getItem('live_russia_questions')) || [];
        ticketsData = JSON.parse(localStorage.getItem('live_russia_tickets')) || [];
        protocolsData = JSON.parse(localStorage.getItem('live_russia_protocols')) || [];
        faqData = JSON.parse(localStorage.getItem('live_russia_faq')) || [];
        const session = localStorage.getItem('live_russia_session');
        if (session) {
            currentUser = JSON.parse(session);
            if (!users.find(u => u.id === currentUser.id)) { currentUser = null; localStorage.removeItem('live_russia_session'); }
        }
    } catch(e) { console.error('Ошибка загрузки:', e); }
}

function saveAllData() {
    localStorage.setItem('live_russia_users', JSON.stringify(users));
    localStorage.setItem('live_russia_news', JSON.stringify(newsData));
    localStorage.setItem('live_russia_gallery', JSON.stringify(galleryData));
    localStorage.setItem('live_russia_wanted', JSON.stringify(wantedData));
    localStorage.setItem('live_russia_wanted_cars', JSON.stringify(wantedCarsData));
    localStorage.setItem('live_russia_leadership', JSON.stringify(leadershipData));
    localStorage.setItem('live_russia_contacts', JSON.stringify(contactsData));
    localStorage.setItem('live_russia_stats', JSON.stringify(statsData));
    localStorage.setItem('live_russia_questions', JSON.stringify(questionsData));
    localStorage.setItem('live_russia_tickets', JSON.stringify(ticketsData));
    localStorage.setItem('live_russia_protocols', JSON.stringify(protocolsData));
    localStorage.setItem('live_russia_faq', JSON.stringify(faqData));
    if (currentUser) localStorage.setItem('live_russia_session', JSON.stringify(currentUser));
    else localStorage.removeItem('live_russia_session');
}

// ... (default данные такие же, как в предыдущих версиях, без изменений)

// ============================================================
// 3. ПРОВЕРКА ПРАВ
// ============================================================

function isAdmin(){return currentUser && currentUser.role === 'admin'}
function isLeader(){return currentUser && currentUser.role === 'leader'}
function isAdminOrLeader(){return currentUser && (currentUser.role === 'admin' || currentUser.role === 'leader')}
function canManageWanted(){return currentUser && (currentUser.role === 'admin' || currentUser.role === 'pingvin')}
function hasExamAccess(){return currentUser && currentUser.examAccess === true}
function canManageProtocols(){return currentUser && (currentUser.role === 'admin' || currentUser.role === 'pingvin')}
function canManageFaq(){return isAdminOrLeader()}

// ============================================================
// 4. НАВИГАЦИЯ И ОБНОВЛЕНИЕ UI
// ============================================================

function navigateTo(page){
    document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
    const target=document.getElementById('page-'+page);
    if(target) target.classList.add('active');
    document.querySelectorAll('.nav-links a').forEach(a=>a.classList.remove('active'));
    document.querySelectorAll('.nav-links a[data-page="'+page+'"]').forEach(a=>a.classList.add('active'));
    if(page==='profile') renderProfile();
    if(page==='admin') updateAdminPanel();
    if(page==='news') renderNews();
    if(page==='gallery') renderGallery();
    if(page==='home') renderHomeNews();
    if(page==='wanted'){renderWantedPersons();renderWantedCars();}
    if(page==='protocols') renderProtocols();
    if(page==='faq') renderFaq();
    if(page==='leadership') renderLeadership();
    if(page==='contacts') renderContacts();
    if(page==='exams'){renderTickets();renderQuestions();}
    updateUI();
}

function updateUI(){
    const ia=isAdminOrLeader(), canM=canManageWanted(), exam=hasExamAccess(), canP=canManageProtocols(), canF=canManageFaq();
    document.getElementById('addNewsBtn').style.display=ia?'inline-block':'none';
    document.getElementById('addGalleryBtn').style.display=ia?'inline-block':'none';
    document.getElementById('editStatsBtn').style.display=ia?'inline-block':'none';
    document.getElementById('addLeaderBtn').style.display=ia?'inline-block':'none';
    document.getElementById('editContactsBtn').style.display=ia?'inline-block':'none';
    document.getElementById('adminNavLink').style.display=ia?'block':'none';
    document.getElementById('addWantedBtn').style.display=canM?'inline-block':'none';
    document.getElementById('addWantedCarBtn').style.display=canM?'inline-block':'none';
    document.getElementById('examNavLink').style.display=exam?'block':'none';
    document.getElementById('footerExamLink').style.display=exam?'block':'none';
    document.getElementById('createTicketBtn').style.display=ia?'inline-block':'none';
    document.getElementById('examQuestionsTab').style.display=ia?'block':'none';
    document.getElementById('addProtocolBtn').style.display=canP?'inline-block':'none';
    document.getElementById('faqManageTab').style.display=canF?'block':'none';
    updateAuthBtn();
}

function updateAuthBtn(){
    const btn=document.getElementById('authBtn'), txt=document.getElementById('authBtnText');
    if(currentUser){txt.textContent=currentUser.fullName||currentUser.username; btn.innerHTML='<i class="fas fa-user-circle"></i> '+txt.textContent;}
    else{txt.textContent='Войти'; btn.innerHTML='<i class="fas fa-user-circle"></i> Войти';}
}

// ============================================================
// 5. РЕГИСТРАЦИЯ, ВХОД, ПРОФИЛЬ (с добавлением FAQ в личном кабинете)
// ============================================================

function registerUser(){
    const fullName=document.getElementById('regFullName').value.trim();
    const email=document.getElementById('regEmail').value.trim();
    const username=document.getElementById('regUsername').value.trim();
    const password=document.getElementById('regPassword').value;
    const confirm=document.getElementById('regPasswordConfirm').value;
    const errorEl=document.getElementById('regError'), successEl=document.getElementById('regSuccess');
    errorEl.style.display='none'; successEl.style.display='none';
    if(!fullName||!email||!username||!password||!confirm){errorEl.textContent='⚠️ Заполните все поля'; errorEl.style.display='block'; return;}
    if(!email.includes('@')||!email.includes('.')){errorEl.textContent='⚠️ Введите корректный email'; errorEl.style.display='block'; return;}
    if(password.length<6){errorEl.textContent='⚠️ Пароль должен быть не менее 6 символов'; errorEl.style.display='block'; return;}
    if(password!==confirm){errorEl.textContent='⚠️ Пароли не совпадают'; errorEl.style.display='block'; return;}
    if(users.find(u=>u.email.toLowerCase()===email.toLowerCase())){errorEl.textContent='⚠️ Пользователь с таким email уже существует'; errorEl.style.display='block'; return;}
    if(users.find(u=>u.username.toLowerCase()===username.toLowerCase())){errorEl.textContent='⚠️ Пользователь с таким логином уже существует'; errorEl.style.display='block'; return;}
    const role=users.length===0?'admin':'user';
    const newUser={id:Date.now(),fullName,email,username,password,role,examAccess:false,createdAt:new Date().toISOString()};
    users.push(newUser); saveAllData();
    successEl.textContent='✅ Регистрация успешна! Теперь войдите.'; successEl.style.display='block';
    document.getElementById('regFullName').value=''; document.getElementById('regEmail').value=''; document.getElementById('regUsername').value=''; document.getElementById('regPassword').value=''; document.getElementById('regPasswordConfirm').value='';
    showToast('🎉 Регистрация успешна!','success');
    setTimeout(()=>{showLoginForm(); showToast('Теперь войдите','info');},1500);
}

function loginUser(){
    const email=document.getElementById('loginEmail').value.trim();
    const password=document.getElementById('loginPassword').value;
    const errorEl=document.getElementById('loginError');
    errorEl.style.display='none';
    if(!email||!password){errorEl.textContent='⚠️ Введите email и пароль'; errorEl.style.display='block'; return;}
    const user=users.find(u=>u.email.toLowerCase()===email.toLowerCase() && u.password===password);
    if(!user){errorEl.textContent='⚠️ Неверный email или пароль'; errorEl.style.display='block'; return;}
    currentUser={id:user.id,fullName:user.fullName,email:user.email,username:user.username,role:user.role,examAccess:user.examAccess};
    saveAllData();
    document.getElementById('loginEmail').value=''; document.getElementById('loginPassword').value='';
    showToast('👋 Добро пожаловать, '+(currentUser.fullName||currentUser.username)+'!','success');
    renderProfile(); updateUI(); navigateTo('profile');
}

function logoutUser(){if(confirm('Вы уверены, что хотите выйти?')){currentUser=null; localStorage.removeItem('live_russia_session'); showToast('Вы вышли из системы','info'); renderProfile(); updateUI(); navigateTo('home');}}

function showRegisterForm(){document.getElementById('loginForm').style.display='none'; document.getElementById('registerForm').style.display='block';}
function showLoginForm(){document.getElementById('loginForm').style.display='block'; document.getElementById('registerForm').style.display='none';}

function renderProfile(){
    const container=document.getElementById('profileContent');
    if(currentUser){
        const roleLabel=currentUser.role==='admin'?'Администратор':currentUser.role==='leader'?'Лидер организации':currentUser.role==='pingvin'?'Пингвин':'Пользователь';
        const roleClass=currentUser.role==='admin'?'admin':currentUser.role==='leader'?'leader':currentUser.role==='pingvin'?'pingvin':'user';
        // Мои протоколы
        const myProtocols = protocolsData.filter(p => p.targetUserId === currentUser.id);
        let protocolsHtml = '';
        if(myProtocols.length === 0){
            protocolsHtml = '<p class="text-muted">Нет протоколов или требований.</p>';
        } else {
            protocolsHtml = myProtocols.map(p => {
                const typeLabels = { protocol: 'Протокол', requirement: 'Требование' };
                const statusLabels = { active: 'Действует', pending: 'На рассмотрении', closed: 'Закрыт' };
                const creator = users.find(u => u.id === p.createdBy);
                const creatorName = creator ? creator.fullName || creator.username : 'Неизвестный сотрудник';
                return `
                    <div class="protocol-card" style="margin-bottom:15px;">
                        <div class="protocol-header">
                            <span><strong>${typeLabels[p.type] || p.type}</strong> №${p.number || '—'}</span>
                            <span class="protocol-status ${p.status || 'active'}">${statusLabels[p.status] || p.status}</span>
                        </div>
                        <div class="protocol-body">
                            <div class="protocol-meta"><i class="fas fa-file-signature"></i> От: ${creatorName}</div>
                            <div class="protocol-meta"><i class="fas fa-book"></i> Статья: ${p.article || 'Не указана'}</div>
                            <div class="protocol-meta"><i class="fas fa-calendar-alt"></i> Дата: ${p.date || 'не указана'}</div>
                            <p style="margin-top:8px;">${p.description || ''}</p>
                        </div>
                    </div>
                `;
            }).join('');
        }
        // Мои вопросы и ответы
        const myFaq = faqData.filter(f => f.userId === currentUser.id);
        let faqHtml = '';
        if(myFaq.length === 0){
            faqHtml = '<p class="text-muted">Вы ещё не задавали вопросов.</p>';
        } else {
            faqHtml = myFaq.map(f => `
                <div class="faq-item" style="margin-bottom:10px;border-left:4px solid ${f.answered ? 'var(--success)' : 'var(--warning)'};">
                    <div class="faq-question"><i class="fas fa-question-circle"></i> ${f.subject}</div>
                    <div class="faq-meta">${f.date}</div>
                    <div>${f.message}</div>
                    ${f.answered ? `<div class="faq-answer"><i class="fas fa-check-circle" style="color:var(--success);"></i> <strong>Ответ:</strong> ${f.answer}</div>` : '<div class="faq-answer" style="background:#fff3cd;border-left-color:var(--warning);">Ожидает ответа</div>'}
                </div>
            `).join('');
        }

        container.innerHTML=`
            <section class="card">
                <div class="profile-card">
                    <div class="profile-avatar"><i class="fas fa-user"></i></div>
                    <div class="profile-name">${currentUser.fullName||currentUser.username}</div>
                    <div class="profile-email"><i class="fas fa-envelope"></i> ${currentUser.email}</div>
                    <span class="role-badge ${roleClass}">${roleLabel}</span>
                    ${currentUser.examAccess?'<span class="role-badge" style="background:var(--success);color:white;margin-left:8px;">Доступ к экзаменам</span>':'<span class="role-badge" style="background:var(--danger);color:white;margin-left:8px;">Нет доступа к экзаменам</span>'}
                </div>
                <div class="profile-stats">
                    <div class="profile-stat" style="background:#f8fafc;padding:15px;border-radius:12px;text-align:center;"><div style="font-size:1.3rem;font-weight:700;color:var(--primary);">12</div><div style="color:var(--text-light);font-size:0.8rem;">Заявлений</div></div>
                    <div class="profile-stat" style="background:#f8fafc;padding:15px;border-radius:12px;text-align:center;"><div style="font-size:1.3rem;font-weight:700;color:var(--primary);">8</div><div style="color:var(--text-light);font-size:0.8rem;">Записей</div></div>
                    <div class="profile-stat" style="background:#f8fafc;padding:15px;border-radius:12px;text-align:center;"><div style="font-size:1.3rem;font-weight:700;color:var(--primary);">0</div><div style="color:var(--text-light);font-size:0.8rem;">Штрафов</div></div>
                </div>
                <div style="margin-top:20px;">
                    <h3><i class="fas fa-file-alt"></i> Мои протоколы и требования</h3>
                    ${protocolsHtml}
                </div>
                <div style="margin-top:20px;">
                    <h3><i class="fas fa-question-circle"></i> Мои вопросы и ответы</h3>
                    ${faqHtml}
                </div>
                <div style="margin-top:20px;display:flex;gap:10px;flex-wrap:wrap;"><button class="btn-secondary" onclick="logoutUser()"><i class="fas fa-sign-out-alt"></i> Выйти</button></div>
            </section>
        `;
    } else {
        container.innerHTML=`
            <section class="card">
                <h2><i class="fas fa-user-plus"></i> Вход / Регистрация</h2>
                <div id="authFormContainer">
                    <div class="auth-form" id="loginForm">
                        <div class="form-group"><label><i class="fas fa-envelope"></i> Email</label><input type="email" id="loginEmail" placeholder="example@mail.ru"></div>
                        <div class="form-group"><label><i class="fas fa-lock"></i> Пароль</label><input type="password" id="loginPassword" placeholder="••••••••"></div>
                        <div id="loginError" class="auth-error"></div>
                        <button class="btn-primary" onclick="loginUser()"><i class="fas fa-sign-in-alt"></i> Войти</button>
                        <div class="form-footer">Нет аккаунта? <a onclick="showRegisterForm()">Зарегистрироваться</a></div>
                        <div class="form-footer" style="margin-top:10px;font-size:0.8rem;color:var(--text-light);"><i class="fas fa-info-circle"></i> Первый пользователь получает права администратора.</div>
                    </div>
                    <div class="auth-form" id="registerForm" style="display:none;">
                        <div class="form-group"><label><i class="fas fa-user"></i> Полное имя</label><input type="text" id="regFullName" placeholder="Иванов Иван Иванович"></div>
                        <div class="form-group"><label><i class="fas fa-envelope"></i> Email</label><input type="email" id="regEmail" placeholder="example@mail.ru"></div>
                        <div class="form-group"><label><i class="fas fa-user-tag"></i> Логин</label><input type="text" id="regUsername" placeholder="ivanov_ivan"></div>
                        <div class="form-group"><label><i class="fas fa-lock"></i> Пароль (минимум 6 символов)</label><input type="password" id="regPassword" placeholder="••••••••"></div>
                        <div class="form-group"><label><i class="fas fa-lock"></i> Подтверждение пароля</label><input type="password" id="regPasswordConfirm" placeholder="••••••••"></div>
                        <div id="regError" class="auth-error"></div>
                        <div id="regSuccess" class="auth-success"></div>
                        <button class="btn-primary" onclick="registerUser()"><i class="fas fa-user-plus"></i> Зарегистрироваться</button>
                        <div class="form-footer">Уже есть аккаунт? <a onclick="showLoginForm()">Войти</a></div>
                    </div>
                </div>
            </section>
        `;
    }
    updateAuthBtn();
}

// ============================================================
// 6. НОВОСТИ, ГАЛЕРЕЯ, СТАТИСТИКА, РАСПИСАНИЕ, РОЗЫСК, ПРОТОКОЛЫ, РУКОВОДСТВО, КОНТАКТЫ – без изменений (опущены для краткости)
// ============================================================

// ... (все эти функции такие же, как в предыдущем коде, они включены в финальный файл)

// ============================================================
// 7. ВОПРОС-ОТВЕТ (FAQ)
// ============================================================

function renderFaq(){
    const askSection = document.getElementById('faqAskSection');
    const manageSection = document.getElementById('faqManageSection');
    // Показываем нужную вкладку
    const activeTab = document.querySelector('.faq-tabs .active');
    if(activeTab && activeTab.textContent.includes('Управление')){
        askSection.style.display = 'none';
        manageSection.style.display = 'block';
        renderFaqManage();
    } else {
        askSection.style.display = 'block';
        manageSection.style.display = 'none';
        renderUserQuestions();
    }
}

function renderUserQuestions(){
    // Отображаем вопросы текущего пользователя
    const container = document.getElementById('userQuestions');
    if(!currentUser){
        container.innerHTML = '<p class="text-muted">Войдите, чтобы задать вопрос.</p>';
        return;
    }
    const myFaq = faqData.filter(f => f.userId === currentUser.id);
    if(myFaq.length === 0){
        container.innerHTML = '<p class="text-muted">Вы ещё не задавали вопросов.</p>';
        return;
    }
    container.innerHTML = myFaq.map(f => `
        <div class="faq-item" style="border-left:4px solid ${f.answered ? 'var(--success)' : 'var(--warning)'};">
            <div class="faq-question"><i class="fas fa-question-circle"></i> ${f.subject}</div>
            <div class="faq-meta">${f.date}</div>
            <div>${f.message}</div>
            ${f.answered ? `<div class="faq-answer"><i class="fas fa-check-circle" style="color:var(--success);"></i> <strong>Ответ:</strong> ${f.answer}</div>` : '<div class="faq-answer" style="background:#fff3cd;border-left-color:var(--warning);">Ожидает ответа</div>'}
        </div>
    `).join('');
}

function renderFaqManage(){
    const container = document.getElementById('faqManageList');
    if(!container) return;
    // Для лидера/админа показываем все неотвеченные или все?
    // Покажем все вопросы, но с возможностью ответить на неотвеченные
    const canManage = canManageFaq();
    if(!canManage){
        container.innerHTML = '<p class="text-muted">Нет прав для управления вопросами.</p>';
        return;
    }
    // Сортируем: сначала неотвеченные
    const sorted = [...faqData].sort((a,b) => (a.answered === b.answered) ? 0 : a.answered ? 1 : -1);
    if(sorted.length === 0){
        container.innerHTML = '<p class="text-muted">Вопросов пока нет.</p>';
        return;
    }
    container.innerHTML = sorted.map(f => {
        const user = users.find(u => u.id === f.userId);
        const userName = user ? user.fullName || user.username : 'Неизвестный';
        return `
            <div class="faq-item" style="border-left:4px solid ${f.answered ? 'var(--success)' : 'var(--warning)'};">
                <div class="faq-question"><i class="fas fa-question-circle"></i> ${f.subject}</div>
                <div class="faq-meta">От: ${userName} | ${f.date}</div>
                <div>${f.message}</div>
                ${f.answered ? `<div class="faq-answer"><i class="fas fa-check-circle" style="color:var(--success);"></i> <strong>Ответ:</strong> ${f.answer}</div>` : ''}
                <div class="faq-actions">
                    ${!f.answered ? `<button class="answer-btn" onclick="openAnswerModal(${f.id})"><i class="fas fa-reply"></i> Ответить</button>` : ''}
                    <button class="delete-btn" onclick="deleteFaq(${f.id})"><i class="fas fa-trash"></i> Удалить</button>
                </div>
            </div>
        `;
    }).join('');
}

function submitQuestion(event){
    event.preventDefault();
    if(!currentUser){
        showToast('Войдите, чтобы задать вопрос','error');
        return;
    }
    const subject = document.getElementById('faqSubject').value.trim();
    const message = document.getElementById('faqMessage').value.trim();
    if(!subject || !message){
        showToast('Заполните все поля','error');
        return;
    }
    faqData.push({
        id: Date.now(),
        userId: currentUser.id,
        subject: subject,
        message: message,
        date: new Date().toLocaleDateString('ru-RU') + ' ' + new Date().toLocaleTimeString('ru-RU', {hour:'2-digit', minute:'2-digit'}),
        answered: false,
        answer: ''
    });
    saveAllData();
    showToast('Вопрос отправлен!','success');
    document.getElementById('faqSubject').value = '';
    document.getElementById('faqMessage').value = '';
    renderFaq();
    updateAdminPanel();
}

function openAnswerModal(faqId){
    const faq = faqData.find(f => f.id === faqId);
    if(!faq) return;
    const html = `
        <h2><i class="fas fa-reply"></i> Ответ на вопрос</h2>
        <div class="auth-form">
            <div class="form-group">
                <label>Вопрос</label>
                <p><strong>${faq.subject}</strong></p>
                <p>${faq.message}</p>
            </div>
            <div class="form-group">
                <label>Ваш ответ</label>
                <textarea id="answerText" rows="4" placeholder="Введите ответ..." required></textarea>
            </div>
            <button class="btn-primary" onclick="submitAnswer(${faq.id})"><i class="fas fa-check"></i> Отправить ответ</button>
            <button class="btn-secondary" style="margin-top:10px;" onclick="closeModal()">Отмена</button>
        </div>
    `;
    openModal('custom', html);
}

function submitAnswer(faqId){
    const answer = document.getElementById('answerText').value.trim();
    if(!answer){
        showToast('Введите ответ','error');
        return;
    }
    const faq = faqData.find(f => f.id === faqId);
    if(faq){
        faq.answer = answer;
        faq.answered = true;
        saveAllData();
        showToast('Ответ отправлен пользователю!','success');
        closeModal();
        renderFaq();
        updateAdminPanel();
    }
}

function deleteFaq(id){
    if(confirm('Удалить этот вопрос?')){
        faqData = faqData.filter(f => f.id !== id);
        saveAllData();
        renderFaq();
        updateAdminPanel();
        showToast('Вопрос удалён','info');
    }
}

function switchFaqTab(tab, btn){
    document.querySelectorAll('.faq-tabs button').forEach(b=>b.classList.remove('active'));
    btn.classList.add('active');
    renderFaq();
}

// ============================================================
// 8. АДМИН-ПАНЕЛЬ (обновлён счётчик FAQ)
// ============================================================

function updateAdminPanel(){
    document.getElementById('totalUsersCount').textContent = users.length;
    document.getElementById('totalNewsCount').textContent = newsData.length;
    document.getElementById('totalWantedCount').textContent = wantedData.length;
    document.getElementById('totalWantedCarsCount').textContent = wantedCarsData.length;
    document.getElementById('totalLeadershipCount').textContent = leadershipData.length;
    document.getElementById('totalQuestionsCount').textContent = questionsData.length;
    document.getElementById('totalTicketsCount').textContent = ticketsData.length;
    document.getElementById('totalGalleryCount').textContent = galleryData.length;
    document.getElementById('totalProtocolsCount').textContent = protocolsData.length;
    document.getElementById('totalFaqCount').textContent = faqData.length;
}

// ============================================================
// 9. УПРАВЛЕНИЕ РОЛЯМИ (добавлена роль "leader")
// ============================================================

function makeLeader(userId){
    if(!isAdmin()){showToast('Доступ запрещен','error');return;}
    const user = users.find(u => u.id === userId);
    if(user){
        user.role = 'leader';
        saveAllData();
        showToast('Пользователь '+(user.fullName||user.username)+' теперь Лидер организации!','success');
        closeModal();
        if(currentUser && currentUser.id === userId){
            currentUser.role = 'leader';
            saveAllData();
            updateUI();
            renderProfile();
        }
        updateAdminPanel();
    }
}

// ============================================================
// 10. МОДАЛЬНОЕ ОКНО (добавлен вызов manageUsers с кнопкой "Лидер")
// ============================================================

function openModal(type, data){
    const modal=document.getElementById('mainModal'), body=document.getElementById('modalBody');
    let html='';
    switch(type){
        // ... остальные case (hotline, addNews, editNews, viewNews, addGallery, viewGallery, editStats, addWanted, editWanted, addWantedCar, editWantedCar, addLeadership, editLeadership, editContacts, addQuestion, addProtocol, editProtocol)
        case 'manageUsers':
            if(!isAdmin()){html=`<p>Доступ запрещен</p><button class="btn-primary" onclick="closeModal()">Закрыть</button>`;}
            else{
                const userList = users.map(u => `
                    <div style="display:flex;justify-content:space-between;align-items:center;padding:10px;border-bottom:1px solid #eef2f7;">
                        <div><strong>${u.fullName||u.username}</strong><br><span style="font-size:0.8rem;color:var(--text-light);">${u.email}</span>
                        <span class="role-badge ${u.role==='admin'?'admin':u.role==='leader'?'leader':u.role==='pingvin'?'pingvin':'user'}">${u.role==='admin'?'Админ':u.role==='leader'?'Лидер':u.role==='pingvin'?'Пингвин':'Пользователь'}</span>
                        ${u.examAccess ? '<span style="font-size:0.7rem;background:var(--success);color:white;padding:1px 8px;border-radius:10px;">Экзамены доступны</span>' : ''}
                        </div>
                        ${u.id!==currentUser.id?`
                            <div style="display:flex;gap:5px;flex-wrap:wrap;">
                                <button class="btn-admin btn-sm" onclick="makeAdmin(${u.id})">Админ</button>
                                <button class="btn-leader btn-sm" onclick="makeLeader(${u.id})">Лидер</button>
                                <button class="btn-admin btn-sm" style="background:var(--pingvin-color);" onclick="makePingvin(${u.id})">Пингвин</button>
                                <button class="btn-secondary btn-sm" onclick="toggleExamAccess(${u.id})">${u.examAccess?'Отключить экзамены':'Включить экзамены'}</button>
                            </div>
                        `:'<span style="color:var(--text-light);font-size:0.8rem;">(Это вы)</span>'}
                    </div>
                `).join('');
                html=`<h2><i class="fas fa-users"></i> Управление пользователями</h2>${users.length===0?'<p class="text-muted">Нет зарегистрированных пользователей</p>':userList}<button class="btn-secondary" style="margin-top:15px;" onclick="closeModal()">Закрыть</button>`;
            }
            break;
        case 'custom':
            html=data;
            break;
        default:
            // остальные case без изменений
            html=`<p>Неизвестное действие</p><button class="btn-primary" onclick="closeModal()">Закрыть</button>`;
    }
    body.innerHTML=html;
    modal.classList.add('active');
    document.body.style.overflow='hidden';
    // обработчики фото и прочее (остаются без изменений)
}

// ============================================================
// 11. ПОИСК, ТЕМА, TOAST, ИНИЦИАЛИЗАЦИЯ
// ============================================================

function searchSite(){
    const q=document.getElementById('searchInput').value.trim();
    if(q){const r=newsData.filter(n=>n.title.toLowerCase().includes(q.toLowerCase())||n.content.toLowerCase().includes(q.toLowerCase())); showToast('🔍 Найдено '+r.length+' результатов','info');}else{showToast('Введите запрос','info');}
}
document.getElementById('searchInput').addEventListener('keypress',function(e){if(e.key==='Enter')searchSite();});

function toggleTheme(){
    const root=document.documentElement;
    const isDark=root.style.getPropertyValue('--bg')==='#1a1a2e';
    if(isDark){root.style.setProperty('--bg','#f0f4fa'); root.style.setProperty('--card-bg','#ffffff'); root.style.setProperty('--text','#2c3e50'); root.style.setProperty('--text-light','#7a8a9e');}
    else{root.style.setProperty('--bg','#1a1a2e'); root.style.setProperty('--card-bg','#252540'); root.style.setProperty('--text','#e8edf3'); root.style.setProperty('--text-light','#a0b0c4');}
}

function showToast(message,type='info'){
    const toast=document.getElementById('toast');
    toast.textContent=message;
    toast.className='toast '+type;
    setTimeout(()=>toast.classList.add('show'),50);
    setTimeout(()=>toast.classList.remove('show'),4000);
}

function closeModal(){document.getElementById('mainModal').classList.remove('active'); document.body.style.overflow='';}
document.getElementById('mainModal').addEventListener('click',function(e){if(e.target===this)closeModal();});

// ============================================================
// 12. ИНИЦИАЛИЗАЦИЯ
// ============================================================

loadAllData();
saveAllData();

document.addEventListener('DOMContentLoaded',function(){
    renderProfile();
    renderNews();
    renderGallery();
    renderHomeNews();
    renderWantedPersons();
    renderWantedCars();
    renderProtocols();
    renderFaq();
    renderLeadership();
    renderContacts();
    renderTickets();
    renderQuestions();
    updateStatsUI();
    updateUI();
    updateAdminPanel();
    showToast('🚗 Добро пожаловать!','info');
});

console.log('🚗 УГИБДД Live Russia загружен!');
console.log('👥 Пользователей:',users.length);
console.log('❓ Вопросов в FAQ:',faqData.length);
</script>
</body>
</html>
