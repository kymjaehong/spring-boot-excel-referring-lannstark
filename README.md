# excel-download
### Fork Git Link
[lannstark](https://github.com/lannstark/excel-download)

<br>

## 클라이언트가 데이터를 Body에 담아 요청
### Controller
```
@RestController
public class ExcelController {

    @PostMapping("/excel/이름")
    public void exportExcelFile(HttpServletResponse response, @RequestBody ExcelLayout<List<DTO>> dto) throws IOException {
        var fileName = "파일명" + ".xlsx";
        response.setHeader(
                "Content-disposition",
                "attachment; filename=" + java.net.URLEncoder.encode(fileName, StandardCharsets.UTF_8));
        response.setContentType("application/vnd.ms-excel");

        ExcelFile<DTO> excelFile = new OneSheetExcelFile<>(dto.getData(), DTO.class);
        excelFile.write(response.getOutputStream());
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
<br>

### ExcelLayout
```
@NoArgsConstructor
@Getter
@ToString
public class ExcelLayout<T> {
    private T data;
}
```