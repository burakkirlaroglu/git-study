# git-study

Elimizdeki commitleri tek commit haline getirmek


Elimizdeki 10 ayrı commit'i tek bir commit haline getirmek için git rebase komutunu kullanabilirsiniz. İşte adım adım nasıl yapılacağına dair bir rehber:

Öncelikle, proje dizininizin bulunduğu dizinde terminal veya komut istemcisini açın.

git log komutunu kullanarak son 10 commit'i inceleyin ve bunların özetini alın. Commit özetlerini görmek için klavyenizdeki "q" tuşunu kullanarak çıkış yapabilirsiniz.

git rebase -i HEAD~10 komutunu çalıştırarak interaktif bir rebase işlemi başlatın. "HEAD~10", son 10 commit'i seçtiğimiz anlamına gelir. Bu komutla bir metin düzenleyici açılacaktır.

Açılan metin düzenleyicisinde, commitlerinizi birleştirmek istediğiniz commitin önündeki "pick" ifadesini "squash" veya "s" ile değiştirin. Örneğin, ilk commiti korumak istiyorsanız, ilk satırdaki "pick" ifadesini "pick" olarak bırakın ve diğer 9 commitin önündeki "pick" ifadelerini "squash" veya "s" ile değiştirin.

Örnek bir metin düzenleyici görünümü:

"""
Copy code
pick abc1234 Birinci commit
s def5678 İkinci commit
s ghi9012 Üçüncü commit
"""

...
Düzenlediğiniz metin düzenleyicisini kaydedin ve kapatın.

Bir sonraki adımda, birleştirmek istediğiniz tüm commitleri tek bir commit haline getirmek için bir başlık ve açıklama belirlemeniz gerekecek. Metin düzenleyicisi, tek bir commit için birleştirilen tüm değişikliklerin açıklamalarını gösterir. Bu açıklamayı düzenleyin ve kaydedin.

Rebase işlemini tamamlamak için metin düzenleyicisini kapatın. Git, commitleri birleştirir ve tek bir commit oluşturur.

Son olarak, projenizi uzak sunucuya veya herhangi bir paylaşılan depoya göndermek isterseniz, git push komutunu kullanarak yapabilirsiniz.

Artık 10 ayrı commit yerine tek bir commit ile devam edebilirsiniz. Ancak bu işlem yerel bir değişikliktir. Eğer proje üzerinde başkaları da çalışıyorsa ve bu commitleri paylaşıyorsanız, dikkatli olmalısınız. Commitleri değiştirmek, paylaşılan bir geçmişin düzeltilmesi anlamına gelir ve diğer işbirliği yapanlarınızı etkileyebilir.




------------------------------------------

git reset komutu, çalışma alanınızı ve özellikle yerel git deposunu düzenlemek için kullanılan güçlü bir Git komutudur. git reset komutunun --hard ve --soft olmak üzere iki yaygın kullanımı vardır ve aralarındaki fark önemlidir:

git reset --hard: Bu seçenek, hem çalışma dizininde hem de yerel depoda yapılan değişiklikleri tamamen geri alır. Yani, tüm çalışma dizinindeki değişiklikler ve son birkaç commit yerel depodan silinir. Bu nedenle bu komutu kullanmadan önce dikkatli olun, çünkü geri alınan değişiklikler geri dönüşü olmayabilir. Kullanımı:

css
Copy code
git reset --hard HEAD
Bu komut, HEAD'i (en son commiti) işaret eder ve çalışma dizinini ve yerel depoyu bu noktaya geri sarmak için --hard seçeneği ile kullanılır.

git reset --soft: Bu seçenek, çalışma dizinindeki değişiklikleri geri alırken, yerel depoda yapılan değişiklikleri korur. Yani, çalışma dizinindeki değişiklikler geri alınır, ancak bu değişikliklerinizi tekrar yeni bir commit olarak eklemek için kullanabilirsiniz. Kullanımı:

css
Copy code
git reset --soft HEAD
Bu komut da HEAD'i işaret eder, ancak --soft seçeneğiyle kullanıldığında, çalışma dizinindeki değişiklikler geri alınırken, yerel depoda bu değişikliklerinizi bekleyen değişiklikler olarak bırakır. Bu nedenle, geri alınan değişiklikleri düzenlemeniz ve yeni bir commit oluşturmanız gerekebilir.

Özetle, git reset --hard, değişiklikleri geri alır ve tüm izleri silerken, git reset --soft, değişiklikleri geri alır ancak bunları yeni bir commit olarak bekletir. Hangi seçeneği kullanmanız gerektiği, yapmak istediğiniz işleme ve değişikliklerinizi nasıl yönetmek istediğinize bağlıdır.


-----------------------------------------


git cherry-pick komutu, başka bir dalda (branch) yapılan belirli bir commit'in değişikliklerini mevcut dalınıza (branch) uygulamanıza olanak tanır. Yani, başka bir dalın commitlerinden yalnızca belirli bir commit'i almak ve bu commit'in değişikliklerini kendi dalınıza eklemek için kullanılır. Bu, özellikle farklı dallardan veya geçmişten belirli bir değişikliği kendi çalışma dalınıza eklemek istediğinizde kullanışlıdır.

git cherry-pick kullanımı aşağıdaki gibidir:

bash
Copy code
git cherry-pick <commit-hash>
<commit-hash>, eklemek istediğiniz commit'in benzersiz kimlik bilgisini ifade eder.
Örnek bir kullanım:

bash
Copy code
git cherry-pick abc1234
Bu komut, abc1234 kimlik bilgisine sahip commit'in değişikliklerini mevcut çalışma dalınıza uygular.

Dikkat edilmesi gereken önemli bir nokta, git cherry-pick işlemi sırasında çakışmalar (conflicts) olabileceğidir. Eğer hedef dalınızda veya hedef commit'inizde değişikliklerle çakışma varsa, Git bu çakışmaları çözmeniz gerektiğini bildirecektir. Çakışmaları çözdükten sonra git add ve git commit komutlarını kullanarak çözünüzü kaydedebilirsiniz.

git cherry-pick komutu, özellikle belirli değişiklikleri diğer dallardan veya geçmişten almak istediğinizde oldukça kullanışlıdır, ancak dikkatli kullanılmalıdır, çünkü geçmişteki commit'lerin sırasını değiştirebilir ve potansiyel olarak çakışmalara yol açabilir.


--------------------------------


git commit -a komutu, değiştirilmiş dosyaları otomatik olarak ekler ve ardından commit işlemini başlatır. Commit işlemi için bir metin düzenleyici açılır ve bu düzenleyiciyi kapatmak ve işlemi tamamlamak için aşağıdaki adımları takip edebilirsiniz:

Eğer bir metin düzenleyici açıldıysa, önce düzenleme yapabilirsiniz. Commit mesajınızı yazın veya düzenleyin.

Düzenlediğiniz metin düzenleyicisini kaydetmek ve kapatmak için, kullanmış olduğunuz metin düzenleyicisinin kaydetme ve çıkma komutlarına bakmalısınız. Genellikle, metin düzenleyicilerinde kullanılan yaygın komutlar şunlardır:

Vim kullanıyorsanız, Esc tuşuna basın, sonra :wq yazıp Enter tuşuna basarak kaydedip çıkabilirsiniz.

Nano kullanıyorsanız, Ctrl + O tuşlarına basarak kaydedebilir ve ardından Ctrl + X tuşlarına basarak çıkabilirsiniz.

Emacs kullanıyorsanız, Ctrl + X, ardından Ctrl + S ile kaydedebilir ve Ctrl + X, ardından Ctrl + C ile çıkabilirsiniz.

Diğer metin düzenleyicileri için kendi kaydetme ve çıkma komutlarını kullanmanız gerekebilir.

Düzenleme işlemini kaydettikten ve metin düzenleyiciyi kapattıktan sonra git commit -a işlemi tamamlanmış olur. Bu adımları takip ederek, git commit -a komutu ile başlattığınız commit işleminden çıkabilirsiniz.


------------------------------------


