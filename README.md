# library.man```mermaid
sequenceDiagram
    title Library Management System – Borrow Book Use Case

    actor Member as Üye
    participant LC as Library Controller
    participant LoanService as Loan Service
    participant BookRepo as Book Repository
    participant LoanRepo as Loan Repository

    Member ->> LC: oduncAl(isbn)
    Note right of Member: Kullanıcı kitap ödünç almak ister

    LC ->> LoanService: borrowBook(memberId, isbn)

    LoanService ->> BookRepo: findBookByIsbn(isbn)
    BookRepo -->> LoanService: Book

    LoanService ->> LoanService: checkAvailability(Book)

    alt Kitap Uygun
        LoanService ->> LoanRepo: createLoan(memberId, isbn)
        LoanRepo -->> LoanService: LoanRecord

        LoanService ->> BookRepo: updateBookStatus(isbn, ODUNCTE)
        LoanService -->> LC: success()

        LC -->> Member: "Ödünç alma işlemi başarıyla tamamlandı"
    else Kitap Uygun Değil
        LoanService -->> LC: failure("Kitap şu anda ödünçte")
        LC -->> Member: "Kitap müsait değil"
    end
```gement.system-ileyda.aky-z
