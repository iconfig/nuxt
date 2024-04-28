<template>
    <div class="w-[375px] relative pb-[53px]" ref="scrollDiv">
<!--        bg-[url('@/assets/intelligent_head_bg.png')]-->
        <div class="pt-[2.4vh]  bg-cover bg-no-repeat h-[92px]">
            <van-nav-bar left-arrow title="智能客服" :border="false" @click-left="onClickLeft" >
                <template #left>
                    <svg-icon class="text-[20px]" name="jiantou"></svg-icon>
                </template>
                <template #right>
                    <svg-icon class="text-[18px]" name="message_icon"></svg-icon>
                </template>
            </van-nav-bar>
        </div>
        <div class="px-[24px] pt-[24px] relative w-[100%] " >
            <div class="flex text-[#060c33cc]">
                <img class="w-[32px] h-[32px]" src="@/assets/intelligent_images.png" alt="">
                <div class="ml-[8px]">
                    <p class="text-[12px]">客户服务</p>
                    <div class="px-[15px] py-[12px] text-[16px] shadow-lg shadow-[#0b18620a] mt-[4px] rounded-[4px]">
                        Hi，尊敬的客户，您好~
                    </div>
                </div>
            </div>
            <div class="border border-[#F7F9FB] rounded-[4px] mt-[24px] pl-[12px] pt-[16px]">
                <h3 class="font-bold text-[14px] text-[#060c33cc]">猜你想问</h3>
                <div class="flex gap-[8px] mt-[8px]">
                    <div class="w-[96px] h-[27px] bg-[#32c8f319] text-[11px] text-center leading-[27px] text-[#00A8D8]">#用卡服务</div>
                    <div class="w-[96px] h-[27px] bg-[#32c8f319] text-[11px] text-center leading-[27px] text-[#00A8D8]">#热点关注</div>
                    <div class="w-[96px] h-[27px] bg-[#32c8f319] text-[11px] text-center leading-[27px] text-[#00A8D8]">#服务指引</div>
                </div>
                <div class="flex items-center px-[5px] justify-between mt-[25px] mb-[16px]">
                    <p class="text-[#00A8D8] text-[14px]">1、信用卡初始额度</p>
                    <svg-icon class="rotate-180 text-xs" name="jiantou"></svg-icon>
                </div>
                <div class="flex items-center px-[5px] justify-between mt-[25px] mb-[16px]">
                    <p class="text-[#00A8D8] text-[14px]">2、标准信用卡年费</p>
                    <svg-icon class="rotate-180 text-xs" name="jiantou"></svg-icon>
                </div>
                <div class="flex items-center px-[5px] justify-between mt-[25px] mb-[16px]">
                    <p class="text-[#00A8D8] text-[14px]">3、白金信用卡年费</p>
                    <svg-icon class="rotate-180 text-xs" name="jiantou"></svg-icon>
                </div>
                <div class="m-auto  bg-gradient-to-r from-[#32C8F3] to-[#26D8F3] w-[102px] h-[33px] text-center leading-[33px] text-[12px] text-white mb-[18px]">
                    在线客服咨询
                </div>
            </div>
            <div class="text-[#060C3366] text-[12px] text-center mt-[12px]">
                人工客服正在为您服务
            </div>
            <div v-for="(msg, index) in messages" :key="index" class="mb-4 mt-[24px]" >
                <div :class="[msg.isOwn ? 'flex' : 'text-left flex']">
                    <div>
<!--                        <img class="w-[32px] h-[32px] mr-[8px]" v-show="!msg.isOwn" src="@/assets/intelligent_images2.png" alt="">-->
                    </div>
                    <p
                        :class="[msg.isOwn ? 'ml-auto bg-[#32C8F3] text-white' : 'shadow-lg shadow-[#0b18620a]', msg.text.length >= 18 ? 'w-[270px]' : '']"
                        class="text-[14px] rounded-lg px-[10px] py-[8px] "
                        id="anchor"
                        style="white-space: pre-wrap; word-break: break-all;"
                    >
                        {{ msg.text }}
                    </p>
                    <div>
<!--                        <img class="w-[32px] h-[32px] ml-[8px]" v-show="msg.isOwn" src="@/assets/intelligent_images.png" alt="">-->
                    </div>
                </div>
            </div>
        </div>
        <div class="flex items-center fixed bottom-0 bg-white h-[52px] w-[375px]">
            <svg-icon class="text-[24px] mx-[16px]" name="voice"></svg-icon>
            <input
                v-model="newMessage"
                type="text"
                placeholder="请输入聊天内容"
                class="flex-grow px-[12px] border border-gray-300 rounded-full h-[28px] text-[12px] placeholder:text-[#060C331A]"
            />
            <div class="flex" v-show="newMessage===''">
<!--                <svg-icon class="text-[24px] ml-[16px] mr-[12px]" name="expression"></svg-icon>-->
<!--                <svg-icon class="text-[24px] mr-[16px]" name="plusSign"></svg-icon>-->
            </div>

            <div @click="sendMessage" class="w-[60px] text-center text-[14px] bg-blue-500 h-[28px] leading-[28px] mx-[16px] rounded-full text-white" v-show="newMessage!==''">
                发送
            </div>
        </div>
    </div>
</template>

<script setup >
import { ref, onMounted, nextTick } from 'vue'

const onClickLeft = ()=>{

}
// 模拟一些聊天消息
const messages = ref([
    { text: '您好！', isOwn: false },
    { text: '请问我的企业信用卡，咱得咨询服务可以解决我的问题吗？', isOwn: true },
    { text: '麻烦您大概介绍下您企业的相关情况吧！', isOwn: false },
    { text: '麻烦您大概介绍下您企业的相关情况吧！', isOwn: false },
    { text: '麻烦您大概介绍下您企业的相关情况吧！', isOwn: false },
    { text: '麻烦您大概介绍下您企业的相关情况吧！', isOwn: false },
    { text: '麻烦您大概介绍下您企业的相关情况吧！', isOwn: false },

]);
// 用于保存新消息的内容
const newMessage = ref('');
// 发送消息的函数
const sendMessage = () => {
    if (newMessage.value.trim() !== '') {
        scrollToTop()
        // 将新消息添加到消息列表
        messages.value.push({ text: newMessage.value, isOwn: true });
        // 清空输入框
        newMessage.value = '';
    }
};


const scrollToTop = () => {
    window.scrollTo({
        top: document.documentElement.offsetHeight, //回到底部
        left: 0,
        behavior: "smooth", //smooth 平滑；auto:瞬间
    })
}
</script>

<style scoped>
::v-deep .van-nav-bar{
    background: transparent;
    padding-bottom: 5px;
}
</style>