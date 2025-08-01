#### Zebra-Printer_Print_EPC_and TID_Information
## RFIDラベルのTID/EPC情報を印刷、ホストに送信するサンプルZPL

</br>


1. サンプルZPL

    ```
    ^XA   

    ; 文字印刷                       
    ^FO10,050^A0N,25,25^FN1^FS
    ^FO10,100^A0N,25,25^FN2^FS
    ^FO10,150^A0N,25,25^FN3^FS

    ; バーコード印刷
    ^FO350,030^BY2^BCN,50,Y,N,N^FN2^FS
    ^FO350,130^BY2^BCN,50,Y,N,N^FN3^FS

    ; FN1
    ^FN1^FD Zebra Sample! ^FS          

    ; バンク１情報の読み取り
    ^FN2^RFR,H,0,12,1^FS

    ; バンク２情報の読み取り
    ^FN3^RFR,H,0,12,2^FS

    ; HVでホスト出力
    ^FH_^HV1,,,_0D_0A,^FS
    ^FH_^HV2,,EPC: ,_0D_0A,^FS
    ^FH_^HV3,,TID: ,_0D_0A,^FS

    ^XZ                          
    ```

</br>

1. ホスト出力情報

    ```
    Zebra Sample!
    EPC: 39BB3000300833B2DDD90140
    TID: E280113020003919CEE90135
    ```

</br>

1. rfid.log.entries

    ```
    ! U1 getvar "rfid.log.entries"
    "<start>
    Aug-01-2025 10:09:03,R,B12,A1,17,00000000,39BB3000300833B2DDD90140
    Aug-01-2025 10:09:03,R,B12,A1,17,00000000,E280113020003919CEE90135
    <end>
    ```

</br>

### 備考

- ZPLの仕様上、QRに^RFRで取得した情報を代入することはできない。



</br>

### 参考： RFID バンク番号一覧

    <table border="1" cellpadding="8" cellspacing="0">
    <thead>
        <tr>
        <th>メモリバンク名</th>
        <th>番号</th>
        <th>説明</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td>Reserved</td>
        <td>00</td>
        <td>アクセスパスワードとキルパスワードを格納。タグの保護・無効化に使用。</td>
        </tr>
        <tr>
        <td>EPC</td>
        <td>01</td>
        <td>商品識別コード（EPC）を格納。サプライチェーンや在庫管理に使用。</td>
        </tr>
        <tr>
        <td>TID</td>
        <td>02</td>
        <td>チップ固有のID（Tag Identifier）を格納。読み取り専用。</td>
        </tr>
        <tr>
        <td>User</td>
        <td>03</td>
        <td>任意のユーザーデータを格納可能。カスタム情報や履歴管理などに使用。</td>
        </tr>
    </tbody>
    </table>