##以ImageView为例说明View的事件处理机制，ImageView中没有去重写dispatchTouchEvent（ev）

	view上的dispatchTouchEvent（ev）方法
	public boolean dispatchTouchEvent(MotionEvent event) {
        ...
		//mOnTouchListener就是imageView调用setOnTouchListener传递进来的对象
		//onTouch返回值结果由自己重写onTouch决定的，如果返回值为true，那当前if条件满足，直接返回true，即dispatchTouchEvent返回true

		// dispatchTouchEvent返回true，响应所有事件
		// 如果onTouch返回的false，顺序执行onTouchEvent(event)
        if (mOnTouchListener != null && (mViewFlags & ENABLED_MASK) == ENABLED &&
                mOnTouchListener.onTouch(this, event)) {
            return true;
        }
        return onTouchEvent(event);
    }
	
	public void setOnTouchListener(OnTouchListener l) {
        mOnTouchListener = l;
    }
	
	imageView.setOnTouchListener(new OnTouchListener() {
		@Override
		public boolean onTouch(View v, MotionEvent event) {
			Log.i(tag, "ImageView onTouch event = "+event.getAction());
			return true;
		}
	});

	
    public boolean onTouchEvent(MotionEvent event) {
        ...
		//当前控件是否可以被点击，如果可以被点击进入if，返回true，即dispatchTouchEvent（ev）返回true，响应所有事件
		//不可以被点击，不进入if，直接返回false，即dispatchTouchEvent（ev）返回false，不响应所有事件
        if (((viewFlags & CLICKABLE) == CLICKABLE ||
                (viewFlags & LONG_CLICKABLE) == LONG_CLICKABLE)) {
            switch (event.getAction()) {
                case MotionEvent.ACTION_UP:
                   ...
					//点击事件的调用方式，就是回调方法
	                performClick();
	               ...
            return true;
        }

        return false;
    }

	//imageView默认没有可点击的事件，但如果添加以下代码，就给其加上了点击事件
	
	//其实就是调用View中setOnClickListener方法
	 public void setOnClickListener(OnClickListener l) {
		//加上可点击事件
        if (!isClickable()) {
            setClickable(true);
        }
        mOnClickListener = l;
    }


	imageView.setOnClickListener(new OnClickListener() {
		@Override
		public void onClick(View v) {
			//在之前的OnTouchListener中的onTouch方法内部返回false，打印两次
		}
	});

	 public boolean performClick() {
        ....
        if (mOnClickListener != null) {
            ...
			//回调onclick方法
            mOnClickListener.onClick(this);
           ...
        }
        ...
    }