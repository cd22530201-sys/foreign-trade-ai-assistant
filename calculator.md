# 🧮 隆源压滤机专业选型计算器 (2026 Pro版)

基于固相守恒定律与隆源 2024 最新基础数据构建。请根据客户询盘输入真实物料参数。

<div style="border:1px solid #ddd; padding: 20px; border-radius: 8px; background: #fdfdfd; margin-top: 20px;">
   <h3 style="margin-top:0; color:#0366d6;">1. 客户工况参数录入 (Client Parameters)</h3>
   
   <label style="font-weight:bold;">每天处理泥水总量 Q (m³):</label><br>
   <input type="number" id="totalVolume" placeholder="例: 100" style="width:100%; padding:10px; margin:8px 0 15px 0; border:1px solid #ccc; border-radius:4px;"><br>

   <label style="font-weight:bold;">泥水含固率 C (%):</label> <span style="font-size:12px;color:#666;">(决定水里有多少干泥)</span><br>
   <input type="number" id="solidContent" placeholder="例: 5" style="width:100%; padding:10px; margin:8px 0 15px 0; border:1px solid #ccc; border-radius:4px;"><br>

   <label style="font-weight:bold;">预期滤饼含水率 M (%):</label> <span style="font-size:12px;color:#666;">(常规填 75)</span><br>
   <input type="number" id="moisture" placeholder="例: 75" style="width:100%; padding:10px; margin:8px 0 15px 0; border:1px solid #ccc; border-radius:4px;"><br>

   <div style="display:flex; justify-content:space-between;">
      <div style="width:48%;">
          <label style="font-weight:bold;">每天运行时间 (Hours):</label><br>
          <input type="number" id="workHours" placeholder="例: 12" style="width:100%; padding:10px; margin:8px 0 15px 0; border:1px solid #ccc; border-radius:4px;">
      </div>
      <div style="width:48%;">
          <label style="font-weight:bold;">单次过滤周期 (Hours):</label><br>
          <input type="number" id="cycleTime" placeholder="例: 2" style="width:100%; padding:10px; margin:8px 0 15px 0; border:1px solid #ccc; border-radius:4px;">
      </div>
   </div>

   <button onclick="calculateProfessional()" style="background:#0366d6; color:white; padding:12px 20px; border:none; border-radius:4px; font-size:16px; cursor:pointer; width:100%; font-weight:bold;">⚙️ 执行专业物料换算 & 匹配机型</button>

   <div id="result" style="margin-top: 25px; padding: 20px; background: #f0f8ff; border-left: 6px solid #0366d6; display: none; font-size:15px; line-height:1.8;">
   </div>
</div>

<script>
function calculateProfessional() {
    var Q = parseFloat(document.getElementById('totalVolume').value);
    var C_percent = parseFloat(document.getElementById('solidContent').value);
    var M_percent = parseFloat(document.getElementById('moisture').value);
    var workHours = parseFloat(document.getElementById('workHours').value);
    var cycleTime = parseFloat(document.getElementById('cycleTime').value);

    if(!Q || !C_percent || !M_percent || !workHours || !cycleTime) {
        alert("⚠️ 请填完整所有的工况参数！");
        return;
    }

    var C = C_percent / 100; // 含固率
    var M = M_percent / 100; // 含水率
    var rho = 1.15; // 湿泥饼默认比重 1.15 t/m³ (行业经验值)

    // 每天循环次数 N
    var N = workHours / cycleTime;
    
    // 核心公式：V = (Q * C) / ((1 - M) * rho * N)
    // 1. 算出每天绝对干泥重量 (假设泥水比重约为1)
    var drySolidWeight = Q * C; 
    // 2. 算出每天湿泥饼总重量
    var wetCakeWeight = drySolidWeight / (1 - M);
    // 3. 算出每天湿泥饼总体积 (m³)
    var totalCakeVolume = wetCakeWeight / rho;
    // 4. 单次所需滤室容积 (m³)
    var reqVolume = totalCakeVolume / N;

    // 隆源2024基础数据 (节选高频主力机型，1000型、1250型、1500型)
    var models = [
        {name: "XAZ1000-60", area: 60, volume: 0.90},
        {name: "XAZ1000-80", area: 80, volume: 1.20},
        {name: "XAZ1000-100", area: 100, volume: 1.50},
        {name: "XAZ1250-150", area: 150, volume: 2.62},
        {name: "XAZ1250-200", area: 200, volume: 3.50},
        {name: "XAZ1500-250", area: 250, volume: 4.40},
        {name: "XAZ1500-300", area: 300, volume: 5.30},
        {name: "XAZ2000-500", area: 500, volume: 10.0}
    ];

    var bestModel = null;
    for(var i=0; i<models.length; i++) {
        if(models[i].volume >= reqVolume) {
            bestModel = models[i];
            break;
        }
    }

    var resDiv = document.getElementById('result');
    resDiv.style.display = 'block';

    if(bestModel) {
        resDiv.innerHTML = "<h3 style='margin-top:0; color:#28a745;'>✅ 选型运算完成</h3>" +
                           "经过固相物质守恒换算，该客户每次压榨产生的湿泥饼体积为：<strong style='color:red; font-size:18px;'>" + reqVolume.toFixed(2) + " m³</strong><br><hr>" +
                           "🎯 <strong>推荐隆源机型：</strong><span style='color:#0366d6; font-size:22px; font-weight:bold;'>" + bestModel.name + "</span><br>" +
                           "📐 <strong>该机型技术包：</strong>过滤面积 " + bestModel.area + " ㎡ | 额定容积 " + bestModel.volume + " m³<br><br>" +
                           "💡 <strong>外贸回复建议：</strong>可直接向客户报价此型号。若物料含固率波动大，建议保留 15% 容积冗余。";
    } else {
        resDiv.innerHTML = "<h3 style='margin-top:0; color:#dc3545;'>⚠️ 超出单机最大极限</h3>" +
                           "经过换算，单次泥饼体积高达：<strong>" + reqVolume.toFixed(2) + " m³</strong><br>" +
                           "建议方案：必须采用 <strong>" + Math.ceil(reqVolume / 10.0) + " 台</strong> XAZ2000-500 并联运行，请即刻联系技术部出具多台布管方案。";
    }
}
</script>
