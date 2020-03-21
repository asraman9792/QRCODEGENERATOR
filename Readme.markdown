QR Code generator library
=========================


Introduction
------------

This project aims to be the best, clearest QR Code generator library in multiple languages. The primary goals are flexible options and absolute correctness. Secondary goals are compact implementation size and good documentation comments.



Features
--------


Manual parameters:

* User can specify minimum and maximum version numbers allowed, then library will automatically choose smallest version in the range that fits the data
* User can specify mask pattern manually, otherwise library will automatically evaluate all 8 masks and select the optimal one
* User can specify absolute error correction level, or allow the library to boost it if it doesn't increase the version number
* User can create a list of data segments manually and add ECI segments

Optional advanced features (Java only):

* Encodes Japanese Unicode text in kanji mode to save a lot of space compared to UTF-8 bytes
* Computes optimal segment mode switching for text with mixed numeric/alphanumeric/general/kanji parts

More information about QR Code technology and this library's design can be found on the project home page.


Examples
--------

Java language:

    import java.awt.image.BufferedImage;
    import java.io.File;
    import java.util.List;
    import javax.imageio.ImageIO;
    import io.nayuki.qrcodegen.*;
    
    // Simple operation
    QrCode qr0 = QrCode.encodeText("Hello, world!", QrCode.Ecc.MEDIUM);
    BufferedImage img = qr0.toImage(4, 10);
    ImageIO.write(img, "png", new File("qr-code.png"));
    
    // Manual operation
    List<QrSegment> segs = QrSegment.makeSegments("3141592653589793238462643383");
    QrCode qr1 = QrCode.encodeSegments(segs, QrCode.Ecc.HIGH, 5, 5, 2, false);
    for (int y = 0; y < qr1.size; y++) {
        for (int x = 0; x < qr1.size; x++) {
            (... paint qr1.getModule(x, y) ...)
        }
    }


License
-------

Copyright © 2020 Project Nayuki. (MIT License)  



