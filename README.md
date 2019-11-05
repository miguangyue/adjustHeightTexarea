# adjustHeightTexarea
文本框自适应
 使用 <textarea [(ngModel)]="teplaterItem.content" class="data-adjustHeight"
                    data-adjustHeight=""></textarea>
    textareaAdjustHeight() {
        let handles = [];
        let textAreas = $('textarea[data-adjustHeight]');
        for (let i = 0, l = textAreas.length; i < l; i++) {
            let el = textAreas[i];
            let minHeight = el.scrollHeight;
            handles[i] = this.adjustHeightHandle(el, minHeight);
            el.addEventListener('input', handles[i]);
            this.adjustHeight(el, minHeight);
        }
    }
    adjustHeightHandle(e, minHeihgt) {
        return () => {
            this.adjustHeight(e, minHeihgt);
        };
    }
    adjustHeight(textareaElement, minHeight) {
        let outerHeight = parseInt(window.getComputedStyle(textareaElement).height, 10);
        let diff = outerHeight - textareaElement.clientHeight;
        textareaElement.style.height = 0;
        textareaElement.style.height = Math.max(minHeight, textareaElement.scrollHeight + diff) + 'px';
    }
