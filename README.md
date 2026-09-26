🌸');
                return;
            }

            let msg = `أهلاً تهادوا 💕 أريد تأكيد أوردر جديد:%0A`;
            msg += `👤 *الاسم:* ${name}%0A📱 *الهاتف:* ${phone}%0A📍 *العنوان:* ${gov} - ${address}%0A`;
            if(cardMsg) msg += `💌 *كرت الإهداء:* ${cardMsg}%0A`;
            msg += `💳 *طريقة الدفع:* ${payMethod}%0A%0A🛍️ *المنتجات:*%0A`;
            cart.forEach(i => { msg += `- ${i.title} (${i.qty} قطعة) = ${i.price * i.qty} ج.م%0A`; });
            msg += `%0A💰 *الإجمالي الشامل:* ${document.getElementById('finalTotal').innerText}`;

            window.open(`https://wa.me/201097453385?text=${msg}`, '_blank');
            cart = [];
            updateCartUI();
            closeAllDrawers();
            alert('تم تجهيز طلبك وسيتم تحويلك للواتساب للتأكيد 💕');
        }

        // مصادقة جوجل
        function toggleAuth() {
            if(currentUser) {
                auth.signOut().then(()=> alert('تم تسجيل الخروج'));
            } else {
                const provider = new firebase.auth.GoogleAuthProvider();
                auth.signInWithPopup(provider).catch(e => alert('خطأ في التسجيل: ' + e.message));
            }
        }

        // منتدى البنوتات
        function addForumPost() {
            const val = document.getElementById('forumInput').value.trim();
            if(!val) return;
            const container = document.getElementById('forumPosts');
            container.innerHTML = `
                <div class="forum-card">
                    <strong>${currentUser ? currentUser.displayName : 'زائرة لطيفة'}:</strong>
                    <p style="font-size:0.9rem; color:var(--text-dark);">${val}</p>
                </div>
            ` + container.innerHTML;
            document.getElementById('forumInput').value = '';
        }
    </script>
</body>
</html>
