# excel-download
reference : https://github.com/lannstark/excel-download

<br>
### Controller
```
@RestController
@RequiredArgsConstructor
public class ExcelController {
    private final DomainReadService domainReadService;

    @GetMapping("domain/excel-download")
    public void getExcel(HttpServletResponse response) throws IOException {
        // 프론트에서 파일 명 등 지정 가능
        response.setContentType("application/vnd.ms-excel");
        
        List<DTO> data = domainReadService.getExcel();
        ExcelFile<DTO> excel = new OneSheetExcelFile<>(data, DTO.class);
        excel.write(response.getOutputStream());
    }
}
```
<br>

### DTO
```
@Getter
@NoArgsConstructor(access = AccessLevel.PROTECTED)
@AllArgsConstructor
@ToString
public class DTO {

    @ExcelColumn(headerName = "타입",
            headerStyle = @ExcelColumnStyle(excelCellStyleClass = DefaultExcelCellStyle.class, enumName = "BLUE_HEADER")
    )
    private String type;

    @ExcelColumn(headerName = "이름",
            headerStyle = @ExcelColumnStyle(excelCellStyleClass = DefaultExcelCellStyle.class, enumName = "BLUE_HEADER")
    )
    private String name;

    @ExcelColumn(headerName = "전화번호",
            headerStyle = @ExcelColumnStyle(excelCellStyleClass = DefaultExcelCellStyle.class, enumName = "BLUE_HEADER")
    )
    private String phoneNumber;

    @ExcelColumn(headerName = "주소",
            headerStyle = @ExcelColumnStyle(excelCellStyleClass = DefaultExcelCellStyle.class, enumName = "BLUE_HEADER")
    )
    private String address;

}
```

