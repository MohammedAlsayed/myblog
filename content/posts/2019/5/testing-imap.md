---
title: "Testing Imap Server"
date: 2019-05-13T16:14:54+03:00
draft: true
rtl: false
---

# Introduction

I'm trying to integrate a zammad server with an imap server that is hosted locally. So, for this purpose I was testing the dovecot server using telnet.

# Testing

    

    openssl s_client -connect support2:993

    CONNECTED(00000005)
    depth=0 OU = IMAP server, CN = imap.example.com, emailAddress = postmaster@example.com
    verify error:num=18:self signed certificate
    verify return:1
    depth=0 OU = IMAP server, CN = imap.example.com, emailAddress = postmaster@example.com
    verify return:1
    ---
    Certificate chain
    0 s:/OU=IMAP server/CN=imap.example.com/emailAddress=postmaster@example.com
    i:/OU=IMAP server/CN=imap.example.com/emailAddress=postmaster@example.com
    ---
    Server certificate
    -----BEGIN CERTIFICATE-----
    MIICQzCCAaygAwIBAgIJANtnJwLZTWoVMA0GCSqGSIb3DQEBCwUAMFgxFDASBgNV
    BAsMC0lNQVAgc2VydmVyMRkwFwYDVQQDDBBpbWFwLmV4YW1wbGUuY29tMSUwIwYJ
    KoZIhvcNAQkBFhZwb3N0bWFzdGVyQGV4YW1wbGUuY29tMB4XDTE5MDUxMjEyNDE1
    OVoXDTIwMDUxMTEyNDE1OVowWDEUMBIGA1UECwwLSU1BUCBzZXJ2ZXIxGTAXBgNV
    BAMMEGltYXAuZXhhbXBsZS5jb20xJTAjBgkqhkiG9w0BCQEWFnBvc3RtYXN0ZXJA
    ZXhhbXBsZS5jb20wgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGBANHg1hwJf7uq
    vsYrPV9v8zCt+EGS1H7PYOGueMmlE1jM3VJwJ6rIq8jSZcjw4f+6ZbWduJamv2k3
    py7CvH6iklal73foZ/7OjgRBWmY6u2AMoL8R86WZU/fvoJ+vpshADTTWBSlJr6Ro
    Royyq6wRKAOVYlylj76HaxAthEr1fXlLAgMBAAGjFTATMBEGCWCGSAGG+EIBAQQE
    AwIGQDANBgkqhkiG9w0BAQsFAAOBgQC9uykSlR0adirDWqK+4LSgoNbr0WYrdnJV
    9SMZyCsSiaI3yGqPvgv/UxxWXpWIoYbF66wrq0NEUR32euM30SJsm6joi1Ixr8OA
    t/tf4NwMfquxe/xUShjd1SSTmQXQ32HF+56EgRZMTkQyjLmEXJJc5xx2Pq833UKO
    qRodD40bCg==
    -----END CERTIFICATE-----
    subject=/OU=IMAP server/CN=imap.example.com/emailAddress=postmaster@example.com
    issuer=/OU=IMAP server/CN=imap.example.com/emailAddress=postmaster@example.com
    ---
    No client certificate CA names sent
    Server Temp Key: ECDH, P-256, 256 bits
    ---
    SSL handshake has read 1109 bytes and written 326 bytes
    ---
    New, TLSv1/SSLv3, Cipher is ECDHE-RSA-AES256-GCM-SHA384
    Server public key is 1024 bit
    Secure Renegotiation IS supported
    Compression: NONE
    Expansion: NONE
    No ALPN negotiated
    SSL-Session:
        Protocol  : TLSv1.2
        Cipher    : ECDHE-RSA-AES256-GCM-SHA384
        Session-ID: B46B17B14DD525476C29933DD7A61B496A346D12DA5B7CAAB91D9505BB2F90A4
        Session-ID-ctx: 
        Master-Key: A2810BB29D4FE71616BAF92011B285CD2F5B32F21417592E053505395A25015ABF9ADDE0DC8021F08004CB0624F3488C
        TLS session ticket lifetime hint: 300 (seconds)
        TLS session ticket:
        0000 - 34 f5 27 d4 7b d3 c9 a4-46 b6 7e 2e d7 b7 95 b1   4.'.{...F.~.....
        0010 - 4c 4e 62 0d a2 3f 60 27-ee 03 3c 4b 04 fe da 33   LNb..?`'..<K...3
        0020 - 93 ba 01 be 3b 8e 0e 06-30 0b 72 e2 63 81 b5 8b   ....;...0.r.c...
        0030 - 89 d7 12 32 2c f9 89 80-ca 33 46 2f 62 91 43 60   ...2,....3F/b.C`
        0040 - 9b 11 8f aa 09 30 10 16-dc 6b b4 89 7a e4 36 bd   .....0...k..z.6.
        0050 - c9 0e 32 c0 63 36 28 e4-e3 a3 09 30 f0 c4 2a 3c   ..2.c6(....0..*<
        0060 - e6 17 36 73 b1 d3 3c 9c-24 92 e0 a6 75 a9 59 2b   ..6s..<.$...u.Y+
        0070 - cb 20 27 af 7c 8a 87 10-92 e1 78 36 31 85 4f 67   . '.|.....x61.Og
        0080 - 59 9f 96 2a b5 50 ba ed-37 f1 af 8e 3e f5 6b 0f   Y..*.P..7...>.k.
        0090 - df f2 04 fa 89 0a d1 0e-65 7f d2 b8 33 be a3 92   ........e...3...

        Start Time: 1557751959
        Timeout   : 7200 (sec)
        Verify return code: 18 (self signed certificate)
    ---
    * OK [CAPABILITY IMAP4rev1 LITERAL+ SASL-IR LOGIN-REFERRALS ID ENABLE IDLE AUTH=PLAIN] Dovecot ready.
    
    a login "support2" "abc123"
    
    a OK [CAPABILITY IMAP4rev1 LITERAL+ SASL-IR LOGIN-REFERRALS ID ENABLE IDLE SORT SORT=DISPLAY THREAD=REFERENCES THREAD=REFS THREAD=ORDEREDSUBJECT MULTIAPPEND URL-PARTIAL CATENATE UNSELECT CHILDREN NAMESPACE UIDPLUS LIST-EXTENDED I18NLEVEL=1 CONDSTORE QRESYNC ESEARCH ESORT SEARCHRES WITHIN CONTEXT=SEARCH LIST-STATUS BINARY MOVE SNIPPET=FUZZY SPECIAL-USE] Logged in
    
    b select inbox
    
    * FLAGS (\Answered \Flagged \Deleted \Seen \Draft)
    * OK [PERMANENTFLAGS (\Answered \Flagged \Deleted \Seen \Draft \*)] Flags permitted.
    * 4 EXISTS
    * 4 RECENT
    * OK [UIDVALIDITY 1557751991] UIDs valid
    * OK [UIDNEXT 5] Predicted next UID
    b OK [READ-WRITE] Select completed (0.003 + 0.000 + 0.002 secs).
    c list "" *
    * LIST (\HasNoChildren) "." INBOX
    c OK List completed (0.001 + 0.000 secs).
    1 select inbox
    * OK [CLOSED] Previous mailbox closed.
    * FLAGS (\Answered \Flagged \Deleted \Seen \Draft)
    * OK [PERMANENTFLAGS (\Answered \Flagged \Deleted \Seen \Draft \*)] Flags permitted.
    * 4 EXISTS
    * 0 RECENT
    * OK [UIDVALIDITY 1557751991] UIDs valid
    * OK [UIDNEXT 5] Predicted next UID
    1 OK [READ-WRITE] Select completed (0.001 + 0.000 secs).
    
    2 FETCH 1:* (FLAGS INTERNALDATE BODY.PEEK[HEADER.FIELDS (SUBJECT)])
    
    * 1 FETCH (FLAGS (\Seen) INTERNALDATE "12-May-2019 16:18:48 +0300" BODY[HEADER.FIELDS (SUBJECT)] {18}
    Subject: test1

    )
    * 2 FETCH (FLAGS (\Seen) INTERNALDATE "12-May-2019 16:35:36 +0300" BODY[HEADER.FIELDS (SUBJECT)] {18}
    Subject: Test2

    )
    * 3 FETCH (FLAGS (\Seen) INTERNALDATE "12-May-2019 16:37:57 +0300" BODY[HEADER.FIELDS (SUBJECT)] {18}
    Subject: Test1

    )
    * 4 FETCH (FLAGS (\Seen) INTERNALDATE "12-May-2019 17:14:38 +0300" BODY[HEADER.FIELDS (SUBJECT)] {18}
    Subject: Test2

    )
    2 OK Fetch completed (0.003 + 0.000 + 0.002 secs).
    
    3 FETCH 1 BODY[TEXT]
    
    * 1 FETCH (BODY[TEXT] {8}
    test 1
    )
    3 OK Fetch completed (0.001 + 0.000 secs).