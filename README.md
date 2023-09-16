# Git - Çalışması

# Tek Bir Commit'i İndirme (Cherry-Pick)

Eğer bir Git deposundan tek bir commit indirmek istiyorsanız, aşağıdaki adımları takip edebilirsiniz.

1. İlgili Git deposuna gidin.

2. İndirmek istediğiniz commit'in kimlik bilgisini (commit hash) alın. Bu kimlik bilgisi, commit'in benzersiz tanımlayıcısıdır.

3. Aşağıdaki komutu kullanarak, ilgili commit'i mevcut dalınıza indirin:
   
   ```bash
   git cherry-pick <commit-hash>
   ```

Elbette, 10 ayrı commiti tek bir commit haline getirmek için Markdown formatında nasıl yapılacağına dair bir açıklama aşağıda verilmiştir:

### 10 Commit'i Tek Bir Commit Haline Getirme

Bazen, bir dizi küçük ve bağlantılı commit yerine bir ana değişikliği tek bir commit olarak saklamak isteyebilirsiniz. İşte bu işlemi nasıl yapacağınızın adımları:

* **!!!! PR'ın merge edileceği branch ile sync olması önemlidir. Conflict meyadan gelebilir. !!!!**

1. **İlgili Git deposuna gidin**.

2. **10 ayrı commit'i tek bir commit olarak birleştirin**:
   
   ```bash
   git rebase -i HEAD~10
   ```

   Bu komut, son 10 commiti düzenleme modunda açacaktır. Metin düzenleyicisi açılacaktır.

3. **Düzenleme modunda, commitleri birleştirin**:
   
   Metin düzenleyicisinde, birleştirmek istediğiniz commitin önündeki "pick" ifadesini "squash" veya kısaltılmış hali olan "s" ile değiştirin. İlk commiti "pick" olarak bırakabilirsiniz.

   Örnek metin düzenleyici görünümü:
   
   ```
   pick abc1234 Birinci commit
   s def5678 İkinci commit
   s ghi9012 Üçüncü commit
   ```

4. **Commit açıklamalarını düzenleyin**:

   Daha sonra, bu 10 commit için tek bir açıklama girin veya açıklamaları düzenleyin.

5. **Düzenlemeyi kaydedin ve kapatın**.

6. **Yeni tek bir commit oluşturun**:
   
   ```
   git push -f
   ```

   Bu komut, yerel ve uzak dalınızdaki commit geçmişini güncelleyecektir.

Artık 10 ayrı commit yerine tek bir commit ile devam edebilirsiniz. Bu adımları takip ederek, bir dizi küçük commiti tek bir commit haline getirebilirsiniz.


# Git Reset Komutunun --hard ve --soft Seçenekleri Arasındaki Fark

Git'te `git reset` komutu, bir daldaki commit geçmişini değiştirmek veya geri almak için kullanılır. `git reset` komutunun `--hard` ve `--soft` olmak üzere iki yaygın kullanımı vardır ve aralarındaki fark önemlidir:

## `git reset --hard`

- Bu seçenek, hem çalışma dizininde hem de yerel depoda yapılan değişiklikleri tamamen geri alır.
- Tüm çalışma dizinindeki değişiklikler silinir ve tüm dosyalar önceki commit durumuna döner.
- Yerel depodaki referanslar (branch işaretçileri) dağıtılmış olan commit'in kimliğine ayarlanır ve bu nedenle tüm sonraki commitler silinir.
- Kullanıcı, bu işlemi gerçekleştirdikten sonra geri alınan değişiklikleri kurtaramaz. Bu nedenle dikkatli kullanılmalıdır.

## `git reset --soft`

- Bu seçenek, çalışma dizinindeki değişiklikleri geri alırken, yerel depodaki commitleri ve geçmişi korur.
- Tüm çalışma dizinindeki değişiklikler silinir, ancak bu değişiklikler önceki commit durumunda "staged" olarak bekler.
- Yerel depodaki referanslar (branch işaretçileri) aynı kalır ve bu nedenle sonraki commitler etkilenmez.
- Kullanıcı, geri alınan değişiklikleri düzenleyebilir ve yeni bir commit olarak ekleyebilir.

Özetle, `git reset --hard` ile yapılan işlem, değişiklikleri ve geçmişi tamamen siler ve geri alınamaz hale getirirken, `git reset --soft` ile yapılan işlem, değişiklikleri saklar ve kullanıcıya düzenleme ve yeni commit ekleme fırsatı sunar. Bu nedenle, hangi seçeneği kullanmanız gerektiği, yapmak istediğiniz işleme ve değişikliklerinizi nasıl yönetmek istediğinize bağlıdır.


Git ile yeni bir depo (repository) oluşturup bunu uzak bir depoya (remote repository) yüklemek için adım adım bir Markdown belgesi aşağıda verilmiştir:

# Yeni Bir Git Depo Oluşturma ve Uzak Depoya Yükleme

1. **Yeni Bir Git Depo (Repository) Oluşturma**:

   Terminali açın ve depo oluşturmak istediğiniz klasöre gidin. Ardından aşağıdaki komutu kullanarak yeni bir Git depo oluşturun:

   ```bash
   git init
   ```

   Bu komut, yeni bir Git depo oluşturur.

2. **Dosyaları ve Değişiklikleri Ekleyin ve Commit Yapın**:

   Çalışma dizinindeki dosyalarınızı düzenleyin veya yeni dosyalar oluşturun. Ardından bu dosyaları "staged" (hazır) durumuna getirin ve bir commit oluşturun:

   ```bash
   git add .                  # Tüm dosyaları staged durumuna getirir.
   git commit -m "İlk commit" # İlk commit'i oluşturur.
   ```

3. **Uzak Depoyu Ekleyin**:

   Uzak bir depo ile çalışmak için, bu depoyu (örneğin, GitHub veya GitLab gibi) eklemeniz gerekmektedir. Uzak depoya bağlanmak için aşağıdaki komutu kullanabilirsiniz:

   ```bash
   git remote add origin <uzak-depo-URL>
   ```

   `<uzak-depo-URL>` kısmını, uzak depo URL'si ile değiştirin.

4. **Uzak Depoya Yükleme (Push Etme)**:

   Şimdi, yerel deponuzdaki commitleri uzak depoya gönderebilirsiniz. Bunun için aşağıdaki komutu kullanın:

   ```bash
   git push -u origin <branch-no>
   ```

   `-u` seçeneği, yerel dalı uzak dal ile ilişkilendirir ve sonraki push işlemleri için daha kolaylık sağlar. `master` yerine kullanmak istediğiniz dalın adını kullanabilirsiniz.

5. **Kullanıcı Bilgilerini Girmek (Opsiyonel)**:

   İlk kez uzak depoya veri gönderiyorsanız, Git sizden kullanıcı adı ve şifre bilgisi isteyebilir. Bu bilgileri girmeniz gerekebilir.

Bu adımları takip ederek, yeni bir Git depo oluşturabilir ve bu depoyu uzak bir depoya yükleyebilirsiniz. Bu Markdown belgesi, bu işlemi adım adım anlatır ve okuyuculara rehberlik eder.


# Git ile revert işlemi

`git revert`, Git'te geçmişteki bir commit'in değişikliklerini geri almak için kullanılan bir komuttur. `git revert` kullanarak, geçmişte bir hata yapan veya istenmeyen bir değişikliği düzelten yeni bir commit oluşturabilirsiniz. Bu, mevcut dalın (branch) geçmişine geri dönmeden, geçmişteki bir commit'i düzelten bir çözüm eklemenizi sağlar.

`git revert` komutunu kullanmanın temel adımları şunlardır:

1. **Revert Yapılacak Commit'i Belirleme**:

   İlk olarak, geri almak istediğiniz commit'in kimlik bilgisini (commit hash) veya referansını belirlemeniz gerekmektedir. Bu commit, geçmişteki bir değişikliği temsil eder.

2. **Revert İşlemini Gerçekleştirme**:

   Aşağıdaki komutu kullanarak belirlediğiniz commit'i geri alabilirsiniz:

   ```bash
   git revert <commit-hash>
   ```

   `<commit-hash>` kısmını geri almak istediğiniz commit'in kimlik bilgisiyle değiştirin.

   Örneğin:

   ```bash
   git revert abc1234
   ```

   Bu komut, `abc1234` kimlik bilgisine sahip commit'in değişikliklerini geri alacak ve yeni bir commit oluşturacaktır.

3. **Commit Açıklamasını Düzenleme**:

   `git revert` komutu, yeni oluşturulan geri alma commit'i için otomatik bir açıklama oluşturur. Açıklamayı düzenlemek isterseniz, düzenleyebilirsiniz.

4. **Değişiklikleri Kaydetme ve Kapatma**:

   Açıklamayı düzenledikten sonra, metin düzenleyicisini kaydedin ve kapatın. Bazı metin düzenleyicileri, varsayılan olarak bir açıklama sağlar ve kapatmak için farklı kısayollar kullanabilir.

5. **Commit'i Oluşturma**:

   Metin düzenleyicisini kapattıktan sonra, yeni geri alma commit'i otomatik olarak oluşturulur.

6. **Push (İsteğe Bağlı)**:

   Eğer çalıştığınız dalı (branch) uzak bir depoya göndermek isterseniz, bu yeni commit'i uzak depoya `git push` komutu ile gönderebilirsiniz.

`git revert`, geçmişteki bir commit'i geri almak ve bu değişikliği yeni bir commit ile kaydetmek için güvenli bir yol sağlar. Bu sayede, geçmişteki hataları düzeltebilir ve geçmişteki değişiklikleri saklayabilirsiniz.



