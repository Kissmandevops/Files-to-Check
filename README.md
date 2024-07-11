this is a terraform codes for new up amd coming devops eng. to work with. dont hesitate to use it as it a lovly code. 


resource "aws_key_pair" "ssh_key" {
 key_name   = "ec2"
 public_key = file(var.public_key)
}

resource "aws_instance" "this" {
 for_each                    = local.instances
 ami                         = each.value.ami
 instance_type               = each.value.instance_type
 key_name                    = aws_key_pair.ssh_key.key_name
 associate_public_ip_address = true

 tags = {
   Name = each.key
 }
}
