# 3.2.2

**Ejemple de uso:**

```java
import facturae.*;

...

ObjectFactory factory = new ObjectFactory();
Facturae factura = factory.createFacturae(
    factory.createFileHeaderType(
        ModalityType.I,
        InvoiceIssuerTypeType.EM,
        factory.createBatchType(
            "385202101N030960",
            new AmountType().setTotalAmount(784.08),
            new AmountType().setTotalAmount(784.08),
            new AmountType().setTotalAmount(784.08),
            CurrencyCodeType.EUR
        ).setInvoicesCount(1)
    ),
    factory.createPartiesType(
        //Seller
        factory.createBusinessType(
            factory.createTaxIdentificationType(
                PersonTypeCodeType.J,
                ResidenceTypeCodeType.R,
                "XXX16653813"
            )
        ).setLegalEntity(factory.createLegalEntityType()
            .setCorporateName("Corp. Name")
            .setAddressInSpain(factory.createAddressType(
                "Av. Barcelona 155",
                "12345",
                "Barcelona",
                "Barcelona",
                CountryType.ESP
            ))
            .setContactDetails(factory.createContactDetailsType()
                .setContactPersons("Rodriguez Rojo Roger")
                .setTelephone("93123456")
                .setTeleFax("93123457")
                .setWebAddress("www.example.com")
            )
        ),
        //Buyer
        factory.createBusinessType(
            factory.createTaxIdentificationType(
                PersonTypeCodeType.J,
                ResidenceTypeCodeType.R,
                "XXX16653813"
            )
        ).setAdministrativeCentres(factory.createAdministrativeCentresType(Arrays.asList(
            factory.createAdministrativeCentreType()
                .setCentreCode("1234")
                .setRoleTypeCode("01")
                .setAddressInSpain(factory.createAddressType(
                    "Av. Barcelona 155",
                    "12345",
                    "Barcelona",
                    "Barcelona",
                    CountryType.ESP
                )),
            factory.createAdministrativeCentreType()
                .setCentreCode("1589")
                .setRoleTypeCode("02")
                .setAddressInSpain(factory.createAddressType(
                    "Av. Barcelona 156",
                    "12345",
                    "Madrid",
                    "Madrid",
                    CountryType.ESP
                ))
        )))
    ),
    factory.createInvoicesType(Arrays.asList(
        factory.createInvoiceType(
            factory.createInvoiceHeaderType(
                "202101N030960",
                InvoiceDocumentTypeType.FC,
                InvoiceClassType.OO
            ),
            factory.createInvoiceIssueDataType(
                getXmlGregorianCalendar("2021-01-07"),
                CurrencyCodeType.EUR,
                CurrencyCodeType.EUR,
                LanguageCodeType.CA
            )
                .setOperationDate(getXmlGregorianCalendar("2021-01-07"))
                .setPlaceOfIssue(factory.createPlaceOfIssueType("12345"))
                .setInvoicingPeriod(factory.createPeriodDates(
                    getXmlGregorianCalendar("2021-01-07"),
                    getXmlGregorianCalendar("2021-02-07")
                ))
            ,
            factory.createInvoiceTypeTaxesOutputs(Arrays.asList(
                factory.createTaxOutputType(
                    "01",
                    factory.createAmountType().setTotalAmount(648)
                )
                .setTaxAmount(factory.createAmountType().setTotalAmount(136.08))
                .setTaxRate(21)
            )),
            factory.createInvoiceTotalsType()
                .setTotalGrossAmount(648)
                .setTotalGrossAmountBeforeTaxes(648)
                .setTotalGeneralDiscounts(0d)
                .setTotalTaxOutputs(136.08)
                .setTotalTaxesWithheld(0)
                .setInvoiceTotal(784.08)
                .setTotalOutstandingAmount(784.08)
                .setTotalExecutableAmount(784.08)
            ,
            factory.createItemsType(Arrays.asList(
                factory.createInvoiceLineType(
                    "Item 1",
                    factory.createInvoiceLineTypeTaxesOutputs(Arrays.asList(
                        factory.createInvoiceLineTypeTaxesOutputsTax(
                            "01",
                            factory.createAmountType().setTotalAmount(65.75)
                        ).setTaxRate(21)
                    ))
                )
                .setQuantity(100)
                .setUnitPriceWithoutTax(0.0657826)
                .setTotalCost(65.75)
                .setGrossAmount(65.75)
            ))
        )
    ))
);
```