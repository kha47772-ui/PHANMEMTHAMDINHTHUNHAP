
import streamlit as st

# Cấu hình giao diện
st.set_page_config(
    page_title="Tính chỉ số DTI",
    page_icon="🏦",
    layout="centered"
)

st.title("🏦 CÔNG CỤ TÍNH CHỈ SỐ DTI")
st.write("Đánh giá khả năng vay vốn của khách hàng")

st.divider()

# Nhập thông tin khách hàng
st.subheader("1. Nhập thông tin khách hàng")

STV = st.number_input(
    "Số tiền vay (VNĐ)",
    min_value=0,
    value=800_000_000,
    step=10_000_000
)

THV = st.number_input(
    "Thời hạn vay (năm)",
    min_value=1,
    value=5,
    step=1
)

LS = st.number_input(
    "Lãi suất vay (%/năm)",
    min_value=0.0,
    value=12.0,
    step=0.5
)

TN = st.number_input(
    "Thu nhập hàng tháng (VNĐ)",
    min_value=0,
    value=45_000_000,
    step=1_000_000
)

NC = st.number_input(
    "Khoản nợ cũ phải trả hàng tháng (VNĐ)",
    min_value=0,
    value=10_000_000,
    step=1_000_000
)

CPSH = st.number_input(
    "Chi phí sinh hoạt mỗi người/tháng (VNĐ)",
    min_value=0,
    value=4_000_000,
    step=500_000
)

SN = st.number_input(
    "Số người trong gia đình",
    min_value=1,
    value=3,
    step=1
)

# Nút tính toán
if st.button("TÍNH CHỈ SỐ DTI", type="primary",
              use_container_width=True):

    # Chuyển lãi suất từ % sang số thập phân
    lai_suat = LS / 100

    # Tính tiền gốc trả hàng tháng
    tien_goc_thang = STV / (THV * 12)

    # Tính tiền lãi hàng tháng theo công thức ban đầu
    tien_lai_thang = STV * (lai_suat / 12)

    # Tổng nghĩa vụ trả nợ hàng tháng
    tong_no_thang = tien_goc_thang + tien_lai_thang + NC

    # Thu nhập còn lại sau chi phí sinh hoạt
    thu_nhap_con_lai = TN - CPSH * SN

    st.divider()
    st.subheader("2. Kết quả đánh giá")

    # Kiểm tra mẫu số
    if thu_nhap_con_lai <= 0:
        st.error(
            "Không thể tính DTI hợp lệ vì thu nhập "
            "sau chi phí sinh hoạt không lớn hơn 0."
        )

    else:
        # Tính DTI
        DTI = tong_no_thang / thu_nhap_con_lai

        # Hiển thị kết quả
        col1, col2 = st.columns(2)

        with col1:
            st.metric(
                "Chỉ số DTI",
                f"{DTI:.2%}"
            )

        with col2:
            st.metric(
                "Ngưỡng DTI",
                "70%"
            )

        # Kết luận theo yêu cầu
        if DTI < 0.70:
            st.error("❌ KẾT LUẬN: KHÔNG ĐƯỢC VAY")
        else:
            st.success("✅ KẾT LUẬN: ĐƯỢC VAY")

        # Chi tiết tính toán
        with st.expander("Xem chi tiết tính toán"):
            st.write(
                f"**Tiền gốc hàng tháng:** "
                f"{tien_goc_thang:,.0f} VNĐ"
            )

            st.write(
                f"**Tiền lãi hàng tháng:** "
                f"{tien_lai_thang:,.0f} VNĐ"
            )

            st.write(
                f"**Tổng nợ phải trả hàng tháng:** "
                f"{tong_no_thang:,.0f} VNĐ"
            )

            st.write(
                f"**Chi phí sinh hoạt gia đình:** "
                f"{CPSH * SN:,.0f} VNĐ"
            )

            st.write(
                f"**Thu nhập còn lại:** "
                f"{thu_nhap_con_lai:,.0f} VNĐ"
            )

            st.write(
                f"**Công thức:** "
                f"DTI = {tong_no_thang:,.0f} / "
                f"{thu_nhap_con_lai:,.0f}"
            )

st.divider()
st.caption(
    "Lưu ý: Kết quả chỉ mang tính tham khảo theo "
    "quy tắc DTI được thiết lập trong chương trình."
)
