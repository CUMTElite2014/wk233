
# 页面查询
  SELECT cp.PrivilegeMaster AS '角色类型',<br>
      cp.PrivilegeMasterKey AS '类型编号',<br>
      cp.PrivilegeAccess AS '对象类型',<br>
      cp.PrivilegeAccessKey AS '对象编号',<br>
      sm.MenuName AS '菜单名称'<br>
    FROM cf_privilege AS cp<br>
      LEFT JOIN sys_menu AS sm ON cp.PrivilegeAccessKey = sm.MenuID AND cp.PrivilegeAccess = 'Sys_Menu'<br>
    WHERE ((cp.PrivilegeMaster = 'CF_Role'<br>
     AND cp.PrivilegeMasterKey<br>
     IN (SELECT RoleID FROM cf_userrole AS cur<br>
       LEFT JOIN cf_user AS cu ON cur.UserID = cu.UserID WHERE cu.LoginName='test1' ))<br>
    OR<br>
     (cp.PrivilegeMaster = 'CF_User'<br>
     AND cp.PrivilegeMasterKey = (SELECT UserID FROM cf_user WHERE LoginName = 'test1')))<br>
    AND<br>
     cp.PrivilegeOperation = 'Permit' AND cp.PrivilegeAccess = 'Sys_Menu';<br>#
# 查询结果     
     ![](https://github.com/wk09143787/wk233/blob/master/1.jpg)
# 伪代码
     
# 订单操作权限
  SELECT cp.PrivilegeMaster AS '角色类型',<br>
    cp.PrivilegeMasterKey AS '类型编号',<br>
    cp.PrivilegeAccess AS '对象类型',<br>
    cp.PrivilegeAccessKey AS '对象编号',<br>
    sb.BtnName AS '按钮名称'<br>
 FROM cf_privilege AS cp<br>
  LEFT JOIN sys_button AS sb ON cp.PrivilegeAccessKey = sb.BtnID AND cp.PrivilegeAccess = 'Sys_Button'<br>
  LEFT JOIN sys_menu AS sm ON sb.MenuNo = sm.MenuNo<br>
 WHERE ((cp.PrivilegeMaster = 'CF_Role'<br>
     AND cp.PrivilegeMasterKey<br>
     IN (SELECT RoleID FROM cf_userrole AS cur<br>
       LEFT JOIN cf_user AS cu ON cur.UserID = cu.UserID WHERE cu.LoginName='test1' ))<br>
    OR<br>
     (cp.PrivilegeMaster = 'CF_User'<br>
     AND cp.PrivilegeMasterKey = (SELECT UserID FROM cf_user WHERE LoginName = 'test1')))<br>
    AND<br>
     cp.PrivilegeOperation = 'Permit' AND cp.PrivilegeAccess = 'Sys_Button' AND sm.MenuName = '订单';<br>
     
 # 查询结果
![](https://github.com/wk09143787/wk233/blob/master/2.jpg)
# 伪代码
