// File: api/get-invoice-data.js

export default async function handler(request, response) {
    // Lấy ID đơn hàng từ query parameter của URL (ví dụ: ?id=DH-001)
    const { id } = request.query;

    if (!id) {
        return response.status(400).json({ error: 'Thiếu mã đơn hàng (id).' });
    }

    // Lấy các biến môi trường từ Vercel
    const apiKey = process.env.APPSHEET_API_KEY;
    const appId = process.env.APPSHEET_APP_ID;
    
    // !!! QUAN TRỌNG: Thay 'Ten_Bang_Don_Hang' bằng tên bảng chứa đơn hàng của bạn trong AppSheet
    const tableName = 'Ten_Bang_Don_Hang'; 

    if (!apiKey || !appId) {
        return response.status(500).json({ error: 'Cấu hình phía máy chủ bị thiếu (API Key hoặc App ID).' });
    }

    const appSheetApiUrl = `https://api.appsheet.com/api/v2/apps/${appId}/tables/${tableName}/Action`;

    const requestBody = {
        "Action": "Find",
        "Properties": {},
        // !!! QUAN TRỌNG: Thay 'So_Don_Hang' bằng tên cột chứa mã đơn hàng của bạn
        "Rows": [
            { "So_Don_Hang": id }
        ]
    };
    
    try {
        const appSheetResponse = await fetch(appSheetApiUrl, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
                'ApplicationAccessKey': apiKey
            },
            body: JSON.stringify(requestBody)
        });

        if (!appSheetResponse.ok) {
            const errorText = await appSheetResponse.text();
            throw new Error(`Lỗi từ AppSheet API: ${appSheetResponse.status} - ${errorText}`);
        }

        const data = await appSheetResponse.json();

        if (!data || data.length === 0) {
            return response.status(404).json({ error: `Không tìm thấy đơn hàng với mã: ${id}` });
        }
        
        // Lấy dòng dữ liệu đầu tiên tìm được
        const orderData = data[0];

        // *** ÁNH XẠ DỮ LIỆU ***
        // Đây là bước quan trọng để chuyển đổi tên cột từ AppSheet sang tên mà file HTML của bạn đang dùng.
        // !!! QUAN TRỌNG: Bạn cần sửa lại các tên cột ('Ten_Cot_Tu_Appsheet') cho đúng với ứng dụng của bạn.
        const mappedData = {
            orderNumber: orderData['So_Don_Hang'],
            orderDate: orderData['Ngay_Dat'],
            customerName: orderData['Khach_Hang'],
            diaChiKhachHang: orderData['Dia_Chi_Khach_Hang'],
            subtotal: orderData['Thanh_Tien'],
            discount: orderData['Giam_Gia'],
            totalAfterDiscount: orderData['Tong_Tien_Sau_CK'],
            notes: orderData['Ghi_Chu_Chung'],
            productsJson: orderData['Products_JSON'], // Giả định bạn có một cột chứa JSON của danh sách sản phẩm
            bankName: orderData['Ten_Ngan_Hang'],
            accountNumber: orderData['So_Tai_Khoan'],
            accountHolder: orderData['Chu_Tai_Khoan'],
            tenCongTy: orderData['Ten_Cong_Ty'],
            diaChi: orderData['Dia_Chi_Cong_Ty'],
            soDienThoai: orderData['SDT_Cong_Ty'],
            email: orderData['Email_Cong_Ty'],
            website: orderData['Website_Cong_Ty']
        };

        // Trả dữ liệu đã được ánh xạ về cho frontend
        return response.status(200).json(mappedData);

    } catch (error) {
        console.error('Lỗi khi gọi AppSheet API:', error);
        return response.status(500).json({ error: 'Lỗi máy chủ nội bộ.', details: error.message });
    }
}
